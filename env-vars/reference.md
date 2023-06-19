# Azion Environment Variables

Environment variables, also known as env variables or secret variables, are a crucial aspect of software development and deployment. They are used to store sensitive information or configuration settings that should not be hardcoded into the codebase.

## Benefifts of using environment variables

### Security

One of the primary reasons to use env variables is to enhance the security of your project. Sensitive information such as API keys, database credentials, or access tokens can be easily compromised if they are hardcoded in your codebase. By using env variables, you can keep this sensitive information separate from the code and limit access to authorized individuals or systems. This reduces the risk of accidental exposure or unauthorized access to critical data.

### Configuration Flexibility

Env variables enable greater flexibility in configuring your application. Instead of modifying code or recompiling your application to update settings, you can simply change the values of the env variables. This makes it easier to deploy your application across different environments (development, staging, production) or when using different providers (e.g., cloud platforms), as each environment can have its own set of variables.

### Portability

Env variables contribute to the portability of your application. By abstracting configuration details away from the code, you can easily move your application between different environments or platforms without modifying the codebase. This is particularly useful when scaling your application or deploying it in different hosting environments.

### Collaboration

Env variables promote collaboration among team members. Since sensitive information is not exposed directly in the codebase, it's safer to have more than one developer working on the same project.

-- Talvez n mencionar
### Version Control
By excluding sensitive information from the codebase, you can avoid committing secrets to version control systems. This prevents secrets from being inadvertently leaked when sharing code repositories or during code reviews. Instead, only the configuration templates or placeholders for env variables are committed, ensuring the security of sensitive information.

### Compliance
In many cases, organizations need to adhere to compliance standards that regulate the handling of sensitive data. By using env variables, you can meet these compliance requirements by ensuring sensitive information is properly protected, controlled, and auditable.

---

## Environment variables on the Azion platform

You can manage your environment variables on the Azion platform trough [Real-Time Manager (RTM) ](https://manager.azion.com/), [Azion CLI](), and [the Azion API](https://api.azion.com/).

The variables are `key:value` based, such as:

```json
  {
  "key": "MY_ENV_VAR",
  "value": "thisismyvar"
  }
```

### Environment variables through RTM

Through the RTM UI, you're able to access the Environment Variables section on the menu. There you can create, update, list and delete your variables.........

### Environment variables through the Azion API

You can manage your env variables using the API, what makes it possible to implement the methods using a client and automatize your use according to your needs. 

We have the following methods available: 

- [POST](https://stage-variables.azion.com/#/api/api_variables_create)
- [GET](https://stage-variables.azion.com/#/api/api_variables_list)
- [GET by ID](https://stage-variables.azion.com/#/api/api_variables_retrieve)
- [PUT](https://stage-variables.azion.com/#/api/api_variables_update)
- [DELETE](https://stage-variables.azion.com/#/api/api_variables_destroy)

---

### Environment variables through the Azion CLI (isso provavelmente demore um pouco mais para subir)

You can manage your env variables using the CLI (isso provavelmente demore um pouco mais para subir), what makes it possible to implement the methods using a client and automatize your use according to your needs. 

We have the following methods available: 

- [POST](https://stage-variables.azion.com/#/api/api_variables_create)
- [GET](https://stage-variables.azion.com/#/api/api_variables_list)
- [GET by ID](https://stage-variables.azion.com/#/api/api_variables_retrieve)
- [PUT](https://stage-variables.azion.com/#/api/api_variables_update)
- [DELETE](https://stage-variables.azion.com/#/api/api_variables_destroy)

---

## Use env variables inside edge functions

You can retrieve the value of your configured env variable inside an edge function making use of the `Azion.env.get()` interface, passing its key, such as:

```javascript
  const apiSecret = Azion.env.get('API_SERVICE_SECRET')
```

Learn more about the [Environment Variables interface](https://github.com/gabriel-azion/doc-studies-mocks/blob/main/env-vars/api-reference.md).

---

## Limits

| Scope | Limitation | Description |
| - | - | - |
| Value | 32k | The max size of a value is 32k |
| Keys | 100 per client | Each client can have 100 `key:value` variables. |  
---

Didn't find what you were looking for? [Open a support ticket](https://tickets.azion.com/).
