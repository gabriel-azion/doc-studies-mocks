---
title: Manage your personal tokens
description: Manage your personal tokens through Azion CLI.
meta_tags: cli, next, javascript, astro, vue, react, edge computing
namespace: documentation_cli_personal_tokens
menu_namespace: cliMenuAlpha
permalink: /documentation/products/cli/personal-tokens/
---

See the command that enable the management of [personal tokens]() through the Azion CLI.

---

## personal_token create


### Usage

```sh
azion personal_token create --name "newToken" --expiration "9m" 
```

### Optional flags

#### in 

The `--in` option informs the file path to a JSON file containing all attributes of the personal token being created.

**Example**

```sh
{
    "name": "One day token",
    "expires_at": "9m"
}
```

#### help

The `--help` option displays more information about the `create` subcommand.


### Required flags when --in is not informed 

#### description 

The `--description` option the personal token's description.

#### expiration 

The `--expiration` option the personal token's expiration.

**Example** 

```sh 
azion personal_token create --name "xxtoken" --expiration "9m" // months
azion personal_token create --name "xxtoken" --expiration "9d" // days
azion personal_token create --name "xxtoken" --expiration "1y" // year
```

#### name

The `--name` option informs the personal token's name.

---

## personal_token list


### Usage

```sh
azion personal_token list [flags]
```

### Optional flags

#### details

The `--details` option displays all relevant fields when listing.

#### help

The `--help` option displays more information about the `list` subcommand.

--- 

## personal_token delete

### Usage

```sh
azion personal_token delete --id xxxxxx-xxxxx-xxxx-xxxxx-xxxx
```

### Required flags 

#### id

The `--id` informs the unique identifier of the personal token being deleted. 

#### Optional flags

#### help

The `--help` option displays more information about the `delete` subcommand.