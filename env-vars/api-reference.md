---
layout: page-documentation-md
title: Environment Variables interface
description: The Environment Variables interface can be used inside Edge Functions to retrieve environment variables. You can use these variables to interact with backend systems like databases, private APIs, or any authenticated service.
meta_tags: edge function, edge computing, edge firewall, security
namespace: documentation_products_edge_functions_environment_variables
permalink: /documentation/runtime/api-reference/environment-variables/
permalink_pt-br: /documentacao/runtime/api-reference/environment-variables/
menu_namespace: edge-runtime-doc-menu
---

# Environment Variables interface

The Environment Variables interface can be used inside Edge Functions to retrieve environment variables. You can use these variables to interact with backend systems like databases, private APIs, or any authenticated service. These variables can be managed through [Azion CLI](https://www.azion.com/en/documentation/products/cli/variables/).

---

## Syntax

```javascript
  const apiToken = Azion.env.get('API_SERVICE_TOKEN');
```

---

## Parameters

| Parameter | Type | Description |
| - | - | - |
| `key` | string | The key of the variable being accessed |

> **Note**: if the key informed is incorrect, it returns `undefined`.

Find out more about [Environment variables](https://www.azion.com/en/documentation/products/edge-application/edge-functions/environment-variables/).

---

## Return value

A `string` with the value stored at the given variable's key, or `undefined` if the key doesn't exist.

---

## Examples

```javascript
    // Here the environment variables are retrieved and, later on, used
    // to make the connection to the DB through a fetch request. 
    const dbUrl = Azion.env.get('DB_URL');
    const dbKey = Azion.env.get('DB_KEY');

   addEventListener('fetch', event => {
    event.respondWith(handleRequest(event.request));
  });
  
  async function handleRequest(request) {
    
    // In this example, a fetch request is sent to Supabase in order to retrieve a list of names from a pre-defined table.
    // The table must be configured on the supabase platform. You can find its base URL and key there as well.
    const apiUrl = `${supabaseUrl}/rest/v1/names?select=*`;
    const headers = new Headers({
      'Content-Type': 'application/json',
      'apikey': supabaseKey,
      'Authorization': `Bearer ${supabaseKey}`
    });
  
    try {
      const response = await fetch(apiUrl, { headers });
  
      if (!response.ok) {
        throw new Error(String(response.error));
      }
  
      const data = await response.json();
  
      const responseBody = { data };
  
      return new Response(JSON.stringify(responseBody), {
        headers: {
          'Content-Type': 'application/json'
        }
      });
    } catch (error) {
      console.error('Error connecting to Supabase: ', error);
  
      return new Response(`Error connecting to Supabase: ${error}`, {
        status: 500
      });
    }
  }
```

---
