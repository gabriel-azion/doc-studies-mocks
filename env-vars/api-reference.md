# Environment Variables interface

The `Azion.env.get()` interface can be used inside edge functions to retrieve an environment variable or a secret variable. You can use these variables to interact with backend systems like databases, private APIs, or any authenticated service. These variables can be managed through [RTM]() and the [Azion API](), applying the necessary access control.

---

## Syntax

```javascript
  const apiSecret = Azion.env.get('API_SERVICE_SECRET');
```

---

## Parameters

| Parameter | Type | Description |
| - | - | - |
| `key` | string | The key of the env/secret variable being accessed |

> **Note**: if the key informed is incorrect, an error is thrown.

Find out more about [Environment variables]({% tl documentation_products_edge_firewall_env_vars %}).

---

## Return value

`string`: returns the value of the env/secret variable by its key.

---

## Usage

Basic usage of `Azion.env.get()`:

```javascript

    const apiSecret = Azion.env.get('API_SERVICE_SECRET')

    addEventListener("fetch", (event) => {
      // Then implement the logic on which this variable is necessary.

    });
```

---

## Error handling

If an error occurs during the execution of `Azion.env.get()`, an exception may be thrown. Make sure to handle potential errors and provide appropriate error messages or fallback actions in your code.

---

Didn't find what you were looking for? [Open a support ticket](https://tickets.azion.com/).

---

Didn't find what you were looking for? [Open a support ticket](https://tickets.azion.com/).
