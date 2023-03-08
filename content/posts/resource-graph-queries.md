+++ 
draft = false
date = 2023-03-08T18:50:05Z
title = "resource graph queries with powershell (two ways!)"
description = ""
slug = ""
authors = ["dan"]
tags = ["azure", "powershell"]
categories = ["azure", "administration"]
externalLink = ""
series = []
+++

Whilst looking at some intermittent Azure DevOps pipeline failures recently, a colleague of mine realized that we were [being throttled by various Azure APIs](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/request-limits-and-throttling), mainly due to how inefficiently our PowerShell scripts were written.

You know the score, you need to enumerate a particular property from all of the storage accounts deployed within your tenant, so you end up quickly doing something along the lines of:

    foreach ($subscription in Get-AzSubscription) {
        <# $subscription is the current item #>
        foreach ($storageAccount in Get-AzStorageAccount) {
            <# $storageAccount is the current item #>
            $storageAccount.BlahBlahProperty
        }
    }

...now this *just about* does the job if you have a relatively small number of subscriptions + storage accounts, but as soon as you start to scale, you will quickly notice two things:

- The script will take exponentially longer (a.k.a **FOREVER**\*)
- You may start seeing timeout issues that can be traced back to the API throttling mentioned above (Storage account management read operations are limited to 800 per 5 minutes)

\*Anecdotally, I've observed a tenant with approximately 100 subscriptions and 500 storage accounts - this script can take between 15 and 30 mins to run from within an ADO pipeline (private build agent).  Try it yourself using the Measure-Object cmdlet...
  
What's the solution?  Well, it's **resource graph of course!** (Otherwise this blog post would be pretty pointless).

The same results as above can be returned with a simple resource graph query:

    Resources
     where type =~ 'Microsoft.Storage/storageAccounts'
    | where tags['tag with a space']=='Custom value'

How do I run this query (you ask)?  Well there are a few ways (Portal, REST API etc) - but my two favourite ways are:

- Azure PowerShell (AZ) Module
- Native PowerShell

1) Azure PowerShell Module:

        Install-Module -Name Az -AllowClobber
        Connect-AzAccount
        Invoke-AzResourceGraphQuery -Query "Resources | where type =~ 'Microsoft.Storage/storageAccount' | project name, resourceGroup"

2) Native PowerShell:

(First obtain an OAuth2 token):

        $clientId = "client_id" # replace with the Application (client) ID of your Azure AD app
        $tenantId = "tenant_id" # replace with the Directory (tenant) ID of your Azure AD tenant
        $clientSecret = "client_secret" # replace with the secret key of your Azure AD app

        $tokenBody = @{
            grant_type    = "client_credentials"
            client_id     = $clientId
            client_secret = $clientSecret
            resource      = "https://management.azure.com/"
        }

        $tokenUrl = "https://login.microsoftonline.com/$tenantId/oauth2/token"
        $tokenResponse = Invoke-RestMethod -Method Post -Uri $tokenUrl -Body $tokenBody

        $accessToken = $tokenResponse.access_token

Then run the query:

        $queryUrl = "https://management.azure.com/providers/Microsoft.ResourceGraph/resources?api-version=2019-04-01"

        $queryBody = @{
            subscriptions = @($subscriptionId) # replace with the ID of the subscription you want to query
            query = @{
                text = "YOUR_QUERY_HERE" # replace with your Resource Graph query
            }
        }

        $queryHeaders = @{
            Authorization = "Bearer $accessToken"
        }

        $queryResponse = Invoke-RestMethod -Method Post -Uri $queryUrl -Headers $queryHeaders -Body ($queryBody | ConvertTo-Json)


And as you can see - both of these methods return all relevant resources in the tenant in a fraction of the time of the foreach monstrosity above.

Azure Resource Graph - it's the way forward (until MS decides to change it).

Now - it's not all rainbows and unicorns, in the near future i'll be putting together a post on some of the downsides of the gotchas with resource graph...
