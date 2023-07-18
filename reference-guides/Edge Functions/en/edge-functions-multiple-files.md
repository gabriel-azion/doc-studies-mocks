---
title: Edge Functions with multiple files
description: 
meta_tags:
namespace: 
permalink:
---

**Edge Functions** work with a single JavaScript (`.js`) file. In case your Edge Functions has more than one file or uses JavaScript modules, you'll need to bundle those files. 

One of the ways to proceed is to use [Webpack](https://webpack.js.org/), which allows you to bundle JavaScript files into a single file.

> Only JavaScript files are supported.

> We don't support Node/Deno API native, so your code must solve all dependencies.

Learn more about [Azion's Runtime API](/en/documentation/products/edge-application/edge-functions/runtime-apis/javascript/).

Example:

If you have an **Edge Function** that has a module to fetch data:

- The `index.js` has the event listener and imports modules.
- The modules folder has all `modules` that are required by your function.
- The `webpack.config.js` has the configuration of how to bundle your function.

### Requirements

- [NodeJS](https://nodejs.org).
- [webpack-cli](https://www.npmjs.com/package/webpack-cli).

### Bundle and Upload

After you code your function, you need to bundle it using the following command:

`webpack-cli --config webpack.config.js`

It will generate a directory called `dist` with a single file called `main.js`. You need to copy the content of this file and paste it into the [RTM](https://manager.azion.com/).

- File structure:

```
your_function/
  	modules/
  		data.js
  	index.js
  	webpack.config.js
```

- Content:

`index.js`

```js
import fetchData from "./modules/data"
 
addEventListener("fetch", (event) => {
   event.respondWith(fetchData())
})
```

- `modules/data.js`:

```js
async function fetchData() {
   let data = await fetch("https://httpbin.org/get?username=azionuser&name=Azion&last_login=2021-03-10")
   let json = await data.json()
   return new Response(JSON.stringify(json["args"]), {"status": 200})
}
 
export default fetchData
```

- `webpack.config.js`:

The target must be "webworker" and the mode must be "production".

```js
module.exports = {
 target: "webworker",
 entry: "./index.js",
 mode: "production",
}
```
### Generated file

- `dist/main.js`:

```js
(()=>{"use strict";addEventListener("fetch",(t=>{t.respondWith(async function(){let t=await fetch("https://httpbin.org/get?username=azionuser&name=Azion&last_login=2021-03-10"),e=await t.json();return new Response(JSON.stringify(e.args),{status:200})}())}))})();
```

---