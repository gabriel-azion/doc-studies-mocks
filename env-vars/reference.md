---
layout: page-documentation-md
title: Environment variables
description: Environment variables, also known as env variables or secret variables, are a crucial aspect of software development and deployment. They are used to store sensitive information or configuration settings that should not be hardcoded into the codebase.
meta_tags: edge functions, edge computing
namespace: documentation_products_edge_functions
permalink: /documentation/products/edge-functions/environment-variables/
permalink_pt-br: /documentacao/produtos/edge-functions/environment-variables/
---

# Azion Environment Variables

**Environment variables**, also known as env variables or secret variables, are a crucial aspect of software development and deployment. They are used to store sensitive information or configuration settings that should not be hardcoded into the codebase.

## Security

One of the primary reasons to use environment variables is to enhance the security of your project. Sensitive information such as API keys, database credentials, or access tokens can be easily compromised if they are hardcoded in your codebase. By using environment variables, you can keep this sensitive information separate from the code and limit access to authorized individuals or systems. This reduces the risk of accidental exposure or unauthorized access to critical data.

## Configuration Flexibility

Environment variables enable greater flexibility in configuring your application. Instead of modifying code or recompiling your application to update settings, you can simply change the values of the environment variables. This makes it easier to deploy your application across different environments (development, staging, production) or when using different providers (e.g., cloud platforms), as each environment can have its own set of variables.

## Portability

Environment variables contribute to the portability of your application. By abstracting configuration details away from the code, you can easily move your application between different environments or platforms without modifying the codebase. This is particularly useful when scaling your application or deploying it in different hosting environments.

## Collaboration

Environment variables promote collaboration among team members. Since sensitive information is not exposed directly in the codebase, it's safer to have more than one developer working on the same project.

## Version Control
By excluding sensitive information from the codebase, you can avoid committing secrets to version control systems. This prevents secrets from being inadvertently leaked when sharing code repositories or during code reviews. Instead, only the configuration templates or placeholders for environment variables are committed, ensuring the security of sensitive information.

## Compliance
In many cases, organizations need to adhere to compliance standards that regulate the handling of sensitive data. By using environment variables, you can meet these compliance requirements by ensuring sensitive information is properly protected, controlled, and auditable.

---

## Environment variables on the Azion platform

### Azion API

...

### Azion CLI

The command `variables` is available and can be used to manage your environment variables using [Azion CLI](https://www.azion.com/en/documentation/products/cli/).

Learn more about the command on [Variables command and its subcommands](https://www.azion.com/en/documentation/products/cli/variables/)

---

## Environment Variables and Edge Functions

You can retrieve the value of your configured environment variable inside an edge function by making use of the `Azion.env.get()` interface, passing its key, such as:

```javascript
  const apiSecret = Azion.env.get('API_SERVICE_SECRET')
```

Learn more about the [Environment Variables interface](https://www.azion.com/en/documentation/products/edge-application/edge-functions/runtime/api-reference/variables/).

---

## Limits

| Scope | Limitation | Description |
| - | - | - |
| Value | 32k | The max size of a value is 32k |
| Keys | 100 per client | Each account can have 100 `key:value` variables. |  
