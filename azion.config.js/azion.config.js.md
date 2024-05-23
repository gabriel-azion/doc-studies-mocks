
# azion.config.js file

## origin

| Property | Description | Values | Required |
| --- | --- | - | - |
| name | The name of the origin. |  | Yes |
| type | The type of the origin, in this case, it's an object storage.  |  Possible values: `single_origin` (default)` load_balancer`,`live_ingest` or `object_storage` | Required |
| bucket | The name of the bucket in the object storage. |  | Yes for object_storage type origins. |
| prefix | The prefix for the objects in the bucket. |   | No |

## cache

| Property | Description |
| --- | --- |
| name | Name of your cache setting. |
| stale | A boolean indicating whether stale content can be served. |
| queryStringSort | Considers objects with the same query strings as the same cached file regardless of the order of the fields. |
| methods | An object specifying which HTTP methods should be cached. |
| browser | An object specifying the maximum age of the cache in the browser. |
| edge | An object specifying the maximum age of the cache at the edge. |

## rules

| Property | Description |
| --- | --- |
| request | An array of request rules. Each rule has properties like name, match, cache, rewrite, setCookie, setHeaders, forwardCookies, setOrigin, deliver, and runFunction. |
| name | The name of the rule. |
| match | The pattern to match for the rule. |
| cache | The name of the cache to use for the rule. |
| rewrite | An object specifying the match and set properties for rewriting the request. |
| setCookie | A string specifying the Set-Cookie header. |
| setHeaders | A string specifying the headers to set. |
| forwardCookies | A boolean indicating whether cookies should be forwarded. |
| setOrigin | An object specifying the name and type of the origin to set. |
| deliver | A boolean indicating whether the content should be delivered. |
| runFunction | An object specifying the path of the function to run. |

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