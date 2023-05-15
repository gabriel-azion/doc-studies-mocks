---
layout: page-documentation-md
title: Azion Terraform Provider
description: Azion Terraform Provider is an open source project, registered in HashiCorp. Through the Azion SDK for Go, the provider communicates with the Azion APIs, so you can manage your infrastructure hosted on the the Azion platform, locally, as code.
meta_tags: edge, terraform,iac
namespace: documentation_terraform_provider
permalink: /documentation/products/terraform-provider/
permalink_pt-br: /documentacao/produtos/terraform-provider/
---

# Azion Terraform Provider

[Terraform](https://developer.hashicorp.com/terraform/docs) is an infrastructure as code tool that makes it possible to manage your infrastructure efficiently through code. The files created to manage your infrastructure can be reused, versioned and shared, helping you to have a consistent workflow to provision and manage all of your infrastructure throughout its lifecycle.

---

## How does Azion Terraform Provider work?

**Terraform** works based [on providers](https://developer.hashicorp.com/terraform/registry/providers). A provider is responsible for managing the lifecycle of a particular resource type. Providers are implemented as plugins, being separate executable code that can be loaded into Terraform at Runtime.

[Azion Terraform Provider](https://github.com/aziontech/terraform-provider-azion) is an open source project, registered in [HashiCorp](https://www.hashicorp.com/) that uses [the Azion SDK (Go)](https://github.com/aziontech/azionapi-go-sdk) to communicate with the Azion APIs, so you can manage your infrastructure hosted on the the Azion platform, locally, as code.

---

## Process

![Azion Terraform Provider Process](/static/images/uploads/doc/terraformProvider.png)

**Terraform Core** -  The Terraform core communicates to the Azion Terraform Provider.

>**Note**: you must have it installed in your environment, [check how to install it here](https://developer.hashicorp.com/terraform/downloads).

**Azion Terraform Provider** - Built in Go, it communicates with the Azion SDK (Go).

**Azion SDK (Go)** - Communicates with the Azion APIs.

---

## Getting started

In your .tf file, you must set the Azion Terraform Provider as the provider and set its version as well, such as:

```json
    required_providers {
        source = "aziontech/azion"
        version = "0.2.0" // it depends on the version you're willing to use.
    }
```

Now, with the provider configured, it's recommended to configure your [Personal token]({% tl documentation_personal_tokens }):

```json
    provider "azion" {
      api_token  = "token" // Here you place your personal token
    }
```

>**Note**: if the Personal Token is not provided as presented above, a prompt will ask you to inform it when you try to run any Terraform command.

After this steps, you're ready to get started managing your infrastructure using the Azion Terraform Provider.

Here's how you `.tf` will look like, for now:

```json
    required_providers {
            source = "aziontech/azion"
            version = "0.2.0" // it depends on the version you're willing to use.
        }
    provider "azion" {
            api_token  = "token" // Here you place your personal token
     }
```

>**Note**: Currently **Azion Terraform Provider** is available only for managing your [Intelligent DNS zones and records]({% tl documentation_products_intelligent_dns %}).

## Implementation

| Capabilty | Resource | Data source |
| --- | --- | --- |
|  Intelligent DNS Zones | [Managing zones](https://github.com/aziontech/terraform-provider-azion/blob/main/docs/resources/zone.md)| [Consulting zones](https://github.com/aziontech/terraform-provider-azion/blob/main/docs/data-sources/zones.md) |
|  Intelligent DNS Records | [Managing records](https://github.com/aziontech/terraform-provider-azion/blob/main/docs/resources/record.md ) | [Consulting records]( https://github.com/aziontech/terraform-provider-azion/blob/main/docs/data-sources/records.md)|


---

## Related documentation

- [Intelligent DNS]({% tl documentation_products_intelligent_dns %})
- [Azion Go SDK](https://github.com/aziontech/azionapi-go-sdk)