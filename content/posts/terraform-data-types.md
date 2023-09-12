+++ 
draft = false
date = 2023-09-10T15:09:26+01:00
title = "terraform data types"
description = ""
slug = ""
authors = ["dan"]
tags = ["azure", "terraform"]
categories = ["azure", "administration"]
externalLink = ""
series = []
+++

# Brewing Success: Deploying Terraform's Data Types for the Cloud Café in Azure

**Introduction:**
Welcome to the grand opening of the Cloud Café, where the aroma of freshly brewed coffee masks the stench of poorly deployed Azure infrastructure. Today, we're not just serving up skinny, double-vented caramel mocha-lattes; we're crafting the infrastructure in the Cloud Cafe global datacenter using some of Terraform's complex data types — lists, sets, and maps. No barista skills required, just a passion for average coffee and lack of enthusiasm for manual deployments.

### Lists: Organizing the Azure Resources

Let's start with lists (or tuples - the list's immutable twin...):

**Key Features**:

1. **Order Matters**: Lists keep our similar Azure resources organized, indexing our sequenced values (starting with 0).

2. **Duplicates Allowed**: Lists allow us to include values from any data types (as long as ever element is the same type...).

**Use Cases in Azure**: Lists are our go-to for maintaining the precise order of resource provisioning, or for passing ordered values to a resource type

```hcl
# Example List
resource "azurerm_virtual_network" "example" {
  name                = "example-network"
  location            = azurerm_resource_group.example.location
  resource_group_name = azurerm_resource_group.example.name
  address_space       = ["10.0.0.0/16"]          # Here's a list!
  dns_servers         = ["10.0.0.4", "10.0.0.5"] # Here's another one, in case you missed the first one
```

### Sets: Guest List for Secure Access

Sets act as our guest list for Cloud Café's VIP section, ensuring secure access for everyone.

**Key Features:**

1. **No Duplicate Entries:** Sets serve as the bouncers at our Azure security gate, ensuring no duplicate entries for added security.

**Use Cases in Azure:** Sets come in handy when you want to define an unordered set of unique values (i.e. no value is repeated). Sets can be useful when you don't care about the order and want to guarantee uniqueness.

```hcl
# Example Set
variable "network_security_groups" {
  type	  = set(string)
  default = ["web-nsg", "app-nsg", "db-nsg"]
}
```

### Maps: Our Blueprint for Resource Configuration

Maps serve as our blueprint, pairing resource attributes (keys) with their configuration settings (values).

**Key Features:**

1. **Key-Value Precision:** Maps help us pair the right attributes with their configurations, ensuring that each resource is perfectly tailored

**Use Cases in Azure:** Anywhere we need to define a set of Key Value pairs!  Resource Tags is a pretty basic, but common use case.

```hcl
# Example Map
variable "tags" {
  type = map(string)
  default = {
    AppName     = "menu-maker"
    Environment = "production"
  }
}
```
