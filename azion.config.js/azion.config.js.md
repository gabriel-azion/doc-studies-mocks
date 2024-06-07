
# azion.config.js file

The `azion.config.js` file is a configuration file created during the build of the application, based on the chosen preset. Each preset presents a set of default settings. These settings can be replaced by the user. This file is the source of truth for the configuration. In case it's deleted, when the build process is triggered again, the default configuration will be recreated.

The configurations set by this file include: 

- Origins
- Cache Settings
- Rules Engine
- Network List

:::note
The properties and values as default generate when a project is initialized are tested and work properly. In case this file is altered, we no longer guarantee it works properly, so use it wisely.
:::

The following tables explain the properties of this configuration file.

---

## origin

| Property | Type | Error Message |
|----------------|----------------|--------------------------------------------------------------------------------------|
| name | string | The 'name' field must be a string. |
| type | string | The 'type' field must be a string. |
| bucket | string, null | The 'bucket' field must be a string or null. |
| prefix | string, null | The 'prefix' field must be a string or null. |
| addresses | array | The 'address' field must be a string. |
| hostHeader | string | The 'hostHeader' field must be a string. |
| additionalProperties | boolean | No additional properties are allowed in origin item objects. |

:::note
| required | array | The 'name and type' field is required in each origin item. |
| errorMessage | object | The 'origin' field must be an array of objects. |
:::

---

## cache


| Property | Type | Expected values |Error Message |
| --- | --- | --- | --- |
| name | string | | The 'name' field must be a string. |
| stale | boolean | | The 'stale' field must be a boolean. |
| queryStringSort | boolean | | The 'queryStringSort' field must be a boolean. |
| methods -> post | boolean | | The 'post' field must be a boolean. |
| methods -> options | boolean | | The 'options' field must be a boolean. |
| methods -> additionalProperties | boolean | | No additional properties are allowed in the 'methods' object. |
| browser -> maxAgeSeconds | number OR string (mathematical expression) | | The 'maxAgeSeconds' field must be a number or a valid mathematical expression. |
| browser -> additionalProperties | boolean | | No additional properties are allowed in the 'browser' object. |
| browser -> required | array | | The 'maxAgeSeconds' field is required in the 'browser' object. |
| edge -> maxAgeSeconds | number OR string (mathematical expression) | | The 'maxAgeSeconds' field must be a number or a valid mathematical expression. |
| edge -> additionalProperties | boolean | | No additional properties are allowed in the 'edge' object. |
| edge -> required | array | | The 'maxAgeSeconds' field is required in the 'edge' object. |

:::note
| additionalProperties | boolean | No additional properties are allowed in cache item objects. |
| required | array | The 'name' field is required in each cache item. |
| errorMessage | object | The 'cache' field must be an array of objects. |
:::


---

## rules


| Property | Type | Error Message |
|----------------|----------------|---------------------------------------------------------------------------------------------------------------|
| request | object | Object containig request rules properties |
| name | string | The 'name' field must be a string. |
| match | string | The 'match' field must be a string. |
| setOrigin -> name | string | The 'name' field must be a string. |
| setOrigin -> type | string | The 'type' field must be a string. |
| setOrigin -> additionalProperties | boolean | No additional properties are allowed in the 'setOrigin' object. |
| setOrigin -> required | array | The 'name or type' field is required in the 'setOrigin' object. |
| rewrite -> match | string, null | The 'match' field must be a string or null. |
| rewrite -> set | function | The 'set' field must be a function. |
| rewrite -> additionalProperties | boolean | No additional properties are allowed in the 'rewrite' object. |
| rewrite -> required | array | The 'set' field is required in the 'rewrite' object. |
| setHeaders | string, null | The 'setHeaders' field must be a string or null. |
| forwardCookies | boolean, null | The 'forwardCookies' field must be a boolean or null. |
| setCookie | string, null | The 'setCookie' field must be a string or null. |
| deliver | boolean, null | The 'deliver' field must be a boolean or null. |
| runFunction -> path | string | The 'path' field must be a string. |
| runFunction -> name | string, null | The 'name' field can be a string or null. |
| runFunction -> additionalProperties | boolean | No additional properties are allowed in the 'runFunction' object. |
| runFunction -> required | array | The 'path' field is required in the 'runFunction' object. |
| cache | string OR object | The 'cache' field must be either a string or an object with specified properties. |
| cache -> name (when cache is an object) | string | The 'name' field must be a string. |
| cache -> browser_cache_settings_maximum_ttl (when cache is an object) | number, null | The 'browser_cache_settings_maximum_ttl' field must be a number or null. |
| cache -> cdn_cache_settings_maximum_ttl (when cache is an object) | number, null | The 'cdn_cache_settings_maximum_ttl' field must be a number or null. |
| cache -> additionalProperties (when cache is an object) | boolean | No additional properties are allowed in the cache object. |
| cache -> required (when cache is an object) | array | The 'name' field is required in the cache object. |


:::note
| additionalProperties | boolean | No additional properties are allowed in request items. |
| required | array | The 'name and match' fields are required in each request item. |
| errorMessage | object | The 'request' array is required in the 'rules' object. |
:::

---

## network list

| Property | Type | Error Message |
|----------------|----------------|-----------------------------------------------------------------------------------------|
| id | number | The 'id' field must be a number. |
| listType | string | The 'listType' field must be a string. |
| listContent | array | The 'listContent' field must be an array of strings. |


:::note
| additionalProperties | boolean | No additional properties are allowed in network list items. |
| required | array | The 'id, listType and listContent' fields are required in each network list item. |
| errorMessage | object | The 'rules' section are required in the configuration object. |
:::

[For further information, access azion.config.js schema in Vulcan repository](https://api.azion.com/#42279c76-58b3-4ce5-9852-1bce43c89524)

---

## Example

```js 
module.exports = {
    origin: [
      {
        name: 'myneworigin',
        type: 'object_storage',
        bucket: 'blue-courage',
        prefix: '0101010101001',
      },
    ],
    cache: [
      {
        name: 'mycache',
        stale: false,
        queryStringSort: false,
        methods: {
          post: false,
          options: false,
        },
        browser: {
          maxAgeSeconds: 1000 * 5,
        },
        edge: {
          maxAgeSeconds: 1000,
        },
      },
    ],
    rules: {
      request: [
        {
          name: 'name1',
          match: '/rewrite',
          cache: 'mycache',
          rewrite: {
            match: '^(./)([^/])$',
            set: (captured) => `/new/${captured[1]}`, // /original/image.jpg -> /new/image.jpg
          },
          setCookie: '',
          setHeaders: '',
          forwardCookies: false,
        },
        {
            name: 'name1qwqqeweqwe',
            match: '/rewrite',
            cache: 'mycache',
            rewrite: {
              match: '^(./)([^/])$',
              set: (captured) => `/new/${captured[1]}`, // /original/image.jpg -> /new/image.jpg
            },
            setCookie: '',
            setHeaders: '',
            forwardCookies: false,
          },
        {
          name: 'name2',
          match: '/^/_statics/;', // start with /_statics
          setOrigin: {
            name: 'myneworigin',
            type: 'object_storage',
          },
          deliver: true,
        },
        {
          name: 'name3',
          match: '/^compute/;', // start with /compute
          runFunction: {
            path: '.edge/worker.js',
          },
        },
      ],
    },
  };
```