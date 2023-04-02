+++ 
draft = false
date = 2023-03-30T19:00:05Z
title = "resource graph gotchas"
description = ""
slug = ""
authors = ["dan"]
tags = ["azure", "cybersecurity"]
categories = ["azure", "administration"]
externalLink = ""
series = []
+++

Following on from my previous post on [the benefits of Azure Resource Graph](https://blog.dantracey.co.uk/posts/resource-graph-queries/), I thought I should try and provide a bit of balance by highlighting a couple of things to consider.

So, a minor gripe to start with...**there can be a lag between the time a resource is created (or updated), and when this change is reflected in Azure Resource Graph**.  The reason for this delay is in the event-driven backed, wherein the Azure Resource Manager provider responsible for making the change has to notify Resource Graph, which then has to update it's database - which can lead to a short delay (I've seen 15-60min delays at times...).  Additionally, Resource Graph performs scheduled full scans of the environment in order to consolidate its data.  As the Resource Graph also powers the Portal search bar - that explains why there is sometimes a delay in newly created resources appearing in search results!

This delay is obviously not ideal in a couple of scenarios, for example:
- Ephemeral workloads (e.g. ACI / AKS) - where a workload may live for a very short period of time, sometimes Graph does not get updated during the lifecycle of the workload process (which can cause problems in an environment where strict asset controls are implemented).
- CICD pipelines - where you rely on Graph as part of an asynchronous process such as vulnerability scanning during an image build.

For full details on how Resource Graph is kept current, [see the official MS Docs](https://learn.microsoft.com/en-us/azure/governance/resource-graph/overview#how-resource-graph-is-kept-current)

Secondly, (and arguably more importantly) **there are a few cybersecurity aspects to consider with Graph**.

As I spoke about in my previous post, Resource Graph provides unparalleled visibility at scale of Azure resources and their metadata, and as such needs to have some level of control to ensure this data does not end up in the wrong hands. **Not only is this visibility tenant-wide, but if Azure lighthouse is in play, it can include details of all connected tenants, too!**

Anyone with **Read-level access** of a resource (let's say for example, a Key Vault...) can use Azure Resource Graph through the lens of their RBAC-role and enumerate resource properties (in our Key Vault example, this could include Access Policies...) - so this is a huge win for an attacker during their reconnaissance and lateral movement phases ([see Mitre Attack Framework](https://attack.mitre.org/))

[The Resource Graph maintains 14 days of change history](https://learn.microsoft.com/en-us/azure/governance/resource-graph/how-to/get-resource-changes?tabs=azure-cli) for a resource, which can also be useful for an attacker to understand maintenance cycles, patching routines, blackout windows etc, and querying the graph can be performed from may different from clients.

One of the worst things about the Resource Graph is that it has **no logging or auditing whatsoever**.  This means that an attacker (who has established *just* Reader access, remember!) can persist in your environment and quickly, easily and regularly run queries to enumerate your public endpoints, NSG rule sets, vulnerable assets etc - and no one will be any the wiser!

So all in all, Azure Resource Graph is a bit of a double-edged sword.  A powerful, currently under-utilised tool that provides wide visibility.  Proceed with caution!