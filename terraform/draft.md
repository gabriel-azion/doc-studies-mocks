# Azion Terraform Provider

[Terraform](https://developer.hashicorp.com/terraform/docs) is an infrastructure as code tool that makes it possible to manage your infrastructure efficiently through code. The files created to manage your infrastructure can be reused, versioned and shared, helping you to have a consistent workflow to provision and manage all of your infrastructure throughout its lifecycle.

## How does Azion Terraform Provider work?

Terraform works based [on providers](https://developer.hashicorp.com/terraform/registry/providers). A provider is responsible for managing the lifecycle of a particular resource type. Providers are implemented as plugins, being separate executable code that can be loaded into Terraform at Runtime.

[Azion Terraform Provider](https://github.com/aziontech/terraform-provider-azion) is an open source project, registered in [HashiCorp](https://www.hashicorp.com/). Through [the Azion SDK (Go)](https://github.com/aziontech/azionapi-go-sdk), it communicates with the Azion APIs, so you can manage your infrastructure hosted on the the Azion platform, locally, as code.

## Process

![azionterraformprovider](./arch.png "workflow")

**Terraform Core** - You must have it installed in your environment, [check how to install it here](https://developer.hashicorp.com/terraform/downloads). The Terraform core communicates to the Azion Terraform Provider.

**Azion Terraform Provider** - Built in Go, it communicates with the Azion SDK (Go).

**Azion SDK (Go)** - Communicates with the Azion APIs.


## Getting started

In your Terraform file, you must set the Azion Terraform Provider as the provider and set its version as well, such as:

```terraform
    required_providers {
        source = "aziontech/azion"
        version = "0.2.0" // it depends on the version you're willing to use.
    }
```

Now, with the provider configured, it's recommended to configure your Personal token:

```json
    provider "azion" {
      api_token  = "token" // Here you place your personal token
}
```

If the Personal Token is not provided as presented above, a prompt will ask you to inform it when you try to run any Terraform command.

After this steps, you're ready to get started managing your infrastructure using the Azion Terraform Provider.

Here's how you `.tf` will look like, for now:

```
    required_providers {
            source = "aziontech/azion"
            version = "0.2.0" // it depends on the version you're willing to use.
        }
    provider "azion" {
            api_token  = "token" // Here you place your personal token
     }
```

>**Note**: Currently **Azion Terraform Provider** is available only for managing your iDNS zones and records.

## Implementation

| Capabilty | Description   |
|---|---|
|  [iDNS Zones](https://github.com/gabriel-azion/terraform/blob/main/guide-zone.md) | Manage your iDNS zones with Azion Terraform Provider  |
|  [iDNS Records]() | Manage your iDNS records with Azion Terraform Provider  |
|  [Domains]() | work in progress...  |
|  [DNS ]() | work in progress...  |

## See also

- [iDNS]()
- [Azion Go SDK]()
- [Azion CLI]()