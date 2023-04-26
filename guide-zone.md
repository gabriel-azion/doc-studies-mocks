# How to manage your iDNS zones with Azion Terraform Provider

Azion [Intelligent DNS](https://www.azion.com/en/documentation/products/intelligent-dns/) is designed for those that want high performance and high availability for their hosting and their domain. Intelligent DNS is an authoritative DNS solution that allows the customers to manage their domains, zones, and records through a friendly and intuitive interface.

A **DNS zone** is a portion of the DNS namespace that is managed by a particular organization or administrative entity. It contains all of the DNS records for a particular domain or subdomain.

## Requirements

In order to be able to work with Azion Terraform Provider, you need to have:

- [Terraform](https://developer.hashicorp.com/terraform/downloads) installed.
- Access to a [personal token](https://www.azion.com/pt-br/documentacao/produtos/gestao-de-contas/personal-tokens/) on [RTM](https://manager.azion.com/).
- Basic knowledge about Terraform.

### Terraform commands

In this process, the following Terraform commands we'll be used:

| Command | Description   |
|---|---|
|  `terraform init` | Prepares your working directory for other commands.  |
|  `terraform plan` | Shows changes required by the current configuration.  |
|  `terraform apply`| Creates or updates infrastructure.  |
|  `terraform destroy`| Destroy previously-created infrastructure.  |

>**Note**: the `terraform apply` command requires a confirmation from the user, as shown below:

```
    Do you want to perform these actions?
    Terraform will perform the actions described above.
    Only 'yes' will be accepted to approve.

    Enter a value: 
```

Take a look at [Terraform Basic CLI Features](https://developer.hashicorp.com/terraform/cli/commands) to learn more about the commands.

---

## Preparing the environment

Create a `.tf` file, for example:

```bash
    mkdir azionTerraform
    cd azionTerraform
    touch azionTerraformProviderExample.tf
```

In your .tf file, you need to set Azion Terraform Provider as the provider source and choose its version.

```json
    terraform {
      required_providers {
        azion = {
          source = "aziontech/azion"
          version = ">= 0.13"
        }
      }
      required_version = ">= 0.13"
    }
```

Then, you configure your Personal token:

```json
    provider "azion" {
      api_token  = "token" // Here you place your personal token
}
```

>**Note**: all steps from now on will happen inside this .tf file.

---

## 1. Creating an iDNS zone

1. In your .tf file, let's create a resource, for example:

```json
    resource "azion_zone" "idnsZone" {
      zone = {
        domain: "yourdomain.com",
        is_active: true,
        name: "Creating a iDNS zone through Azion Terraform Provider"
      }
    }
    
    output "dev_Azion" {
      value = azion_zone.idnsZone
    }
```

2. Now, with the resource set, we open the current directory in the terminal and run:

```bash
    terraform init
```

3. Then:

```bash
    terraform plan
```

4. To implement the changes:

```bash
    terraform apply
```

Expected output:

```bash
    Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the
    following symbols:
      + create

    Terraform will perform the following actions:

      # azion_zone.dev3 will be created
      + resource "azion_zone" "dev3" {
          + id             = (known after apply)
          + last_updated   = (known after apply)
          + schema_version = (known after apply)
          + zone           = {
              + domain      = "testtalk1.com"
              + expiry      = (known after apply)
              + id          = (known after apply)
              + is_active   = true
              + name        = "test for tech talk terraform"
              + nameservers = (known after apply)
              + nxttl       = (known after apply)
              + refresh     = (known after apply)
              + retry       = (known after apply)
              + soattl      = (known after apply)
            }
        }

    Plan: 1 to add, 0 to change, 0 to destroy.

    Changes to Outputs:
      + dev_Azion = {
          + zone = {
              + domain    = "yourdomain.com"
              + is_active = true
              + name      = "Creating a iDNS zone through Azion Terraform Provider"
            }
        }

    Do you want to perform these actions?
      Terraform will perform the actions described above.
      Only 'yes' will be accepted to approve.

    Enter a value: yes

    azion_zone.dev3: Creating...
    azion_zone.dev3: Creation complete after 1s [id=2726]
```

---

## 2. Updating an iDNS zone

Once you have the resource created in your .tf file, as represented in the creating an iDNS zone section, you're able to alter some values, for example:

1. Changing the name of the recently created :

**Resource created earlier**

```json
    resource "azion_zone" "idnsZone" {
      zone = {
        domain: "yourdomain.com",
        is_active: true,
        name: "Creating a iDNS zone through Azion Terraform Provider"
      }
    }
    
    output "dev_Azion" {
      value = azion_zone.idnsZone
    }
```

**Altering some values**

Let's alter the name of our recently created iDNS zone:

```json
    resource "azion_zone" "idnsZone" {
      zone = {
        domain: "yourdomain.com",
        is_active: true,
        name: "Updating a iDNS zone through Azion Terraform Provider"
      }
    }
    
    output "dev_Azion" {
      value = azion_zone.idnsZone
    }
```

2. Now, with the resource set and the changes implemented, we open the current directory in the terminal and run:

```bash
    terraform init
```

3. Then:

```bash
    terraform plan
```

4. To implement the changes:

```bash
    terraform apply
```

Expected output:

```bash
    azion_zone.dev3: Refreshing state... [id=xxxxx]
    data.azion_zones.dev: Reading...
    data.azion_zones.dev: Read complete after 2s [id=placeholder]
    
    Terraform used the selected providers to generate the following execution plan. Resource actions are indicated with the following symbols:
      ~ update in-place
    
    Terraform will perform the following actions:
    
      # azion_zone.dev3 will be updated in-place
      ~ resource "azion_zone" "dev3" {
            id             = "xxxxx"
          ~ last_updated   = "Wednesday, 26-Apr-23 13:06:29 -03" -> (known after apply)
          ~ schema_version = 3 -> (known after apply)
          ~ zone           = {
              ~ expiry      = 1209600 -> (known after apply)
              ~ id          = xxxxx -> (known after apply)
              ~ name        = "Creating a iDNS zone through Azion Terraform Provider" -> "Updating a iDNS zone through Azion Terraform Provider"
              ~ nameservers = [
                  - "ns1.aziondns.net",
                  - "ns2.aziondns.com",
                  - "ns3.aziondns.org",
                ] -> (known after apply)
              ~ nxttl       = 3600 -> (known after apply)
              ~ refresh     = 43200 -> (known after apply)
              ~ retry       = 7200 -> (known after apply)
              ~ soattl      = 3600 -> (known after apply)
                # (2 unchanged attributes hidden)
            }
        }
    
    Plan: 0 to add, 1 to change, 0 to destroy.
    
    Changes to Outputs:
      ~ dev_Azion = {
            id             = "xxxxx"
          - last_updated   = "Wednesday, 26-Apr-23 13:06:29 -03"
          - schema_version = 3
          ~ zone           = {
              - expiry      = 1209600
              - id          = xxxxx
              ~ name        = "testing" -> "testing name"
              - nameservers = [
                  - "ns1.aziondns.net",
                  - "ns2.aziondns.com",
                  - "ns3.aziondns.org",
                ]
              - nxttl       = 3600
              - refresh     = 43200
              - retry       = 7200
              - soattl      = 3600
                # (2 unchanged attributes hidden)
            }
        }
      ~ dev_zones = {
          ~ counter        = 1 -> 2
            id             = "placeholder"
          ~ results        = [
                {
                    domain    = "aaababa.com"
                    id        = 2662
                    is_active = true
                    name      = "domain.co"
                },
              + {
                  + domain    = "francinha.com"
                  + id        = xxxxx
                  + is_active = true
                  + name      = "testing"
                },
            ]
            # (3 unchanged attributes hidden)
        }
    
    Do you want to perform these actions?
      Terraform will perform the actions described above.
      Only 'yes' will be accepted to approve.
    
      Enter a value: yes
    
    azion_zone.dev3: Modifying... [id=xxxxx]
    azion_zone.dev3: Modifications complete after 2s [id=xxxxx]
```

---

## 3. Listing your iDNS zones

1. In your .tf file, let's list all iDNS zones:

```json
    data "azion_zones" "dev" {
    }

    output "dev_zones" {
      value = data.azion_zones.dev
    }
```

2. Now, with the data set, we open the current directory in the terminal and run:

```bash
    terraform init
```

3. Then:

```bash
    terraform plan
```

4. To implement the changes:

```bash
    terraform apply
```

Expected output: 

```bash
    ...
    ...

    Outputs:
    dev_zones = {
      "counter" = 1
      "id" = "placeholder"
      "links" = {
        "next" = ""
        "previous" = ""
      }
      "results" = tolist([
        {
          "domain" = "yourdomain.com"
          "id" = xxxxxx
          "is_active" = true
          "name" = "Creating a iDNS zone through Azion Terraform Provider"
        }
      ])
      "schema_version" = 3
      "total_pages" = 1
    }
```

---

## 4. Describing an iDNS zone

1. Once you've listed your iDNS zones, you have access to their IDs. Let's define the zone you want to have described by informing its id:

```json
    data "azion_zone" "azionZone" {
      id = "id"
    }
    output "dev_zone" {
    value = data.azion_zone.azionZone
}
```

2. Now, with the data set, we open the current directory in the terminal and run:

```bash
    terraform init
```

3. Then:

```bash
    terraform plan
```

4. To implement the changes:

```bash
    terraform apply
```

Expected output: 

```bash
    Apply complete! Resources: 0 added, 0 changed, 0 destroyed.

    Outputs:

    dev_zone = {
      "id" = "Get By ID Zone"
      "results" = {
        "domain" = "yourdomain.com"
        "expiry" = 1209600
        "is_active" = true
        "name" = "Creating a iDNS zone through Azion Terraform Provider"
        "nameservers" = tolist([
          "ns1.aziondns.net",
          "ns2.aziondns.com",
          "ns3.aziondns.org",
        ])
        "nxttl" = 3600
        "refresh" = 43200
        "retry" = 7200
        "soattl" = 3600
        "zone_id" = 2662
      }
      "schema_version" = 3
    }
```

## 5. Deleting local changes

(inprogress)...
