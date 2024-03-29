# Object Storage API

The [Edge Functions]() storage API is an interface that allows access to Azion Storage. Through this interface, it's possible to write and retrieve data in the Storage.

## Class instantiation

To leverage this API, you need to instantiate the Storage class, passing the version ID.

### Syntax

```js
const storage = Azion.Storage.new(versionId);
```

### Parameters

| Parameter | Type | Description |
| - | - | - |
| `versionId` | string | Key to a group of stored objects. If the key doesn't match any existing version ID, a new one is created. |

### Return value

Storage object used to access Azion Storage

---

## Methods

### async Storage.put

The Storage.put method is used to insert a new object to Azion Storage.

:::note
The method is async, and must be used with await or event.waitUntil.
:::

#### Syntax

```js
async Storage.put(key, value, options)
```

#### Parameters

| Parameter | Type | Description |
| - | - | - |
| `key` | string | Key to a group of stored objects. If the key doesn't match any existing version ID, a new one is created. |
| `value` | string | Key to a group of stored objects. If the key doesn't match any existing version ID, a new one is created. |
| `options` | string | Key to a group of stored objects. If the key doesn't match any existing version ID, a new one is created. |

**options**

To pass the `options` parameter, it's necessary to provide an object with the following attributes:

| Attribute | Type | Description |
| - | - | - |
| `content-type` | string | The content-type of the object to be created. It is similar to the HTTP Header Content-type and describes how the content of the object storage should be treated. Content-type is optional; the default value is application/octet-stream. |
| `content-length` | string | The size of the object to be created in bytes. It is mandatory when the value is ReadableStream. |
| `metadata` | object | Any JavaScript object containing information about the object that will be stored in the Storage. All properties of the object must be strings. |

#### Return

| Success | Error |
|-|-|
| No response| It throws a `StorageError`|

#### Code sample

1. Persisting the request body:

```js
async function handleRequest(event) {
    try{
        const versionId = "v1.0";
        const storage = Azion.Storage.new(versionId);
        const key = "test";
        const inputStream = event.request.body;
        let contentLength = event.request.headers.get("content-length");
        await storage.put(key, inputStream, { "content-length": contentLength });
        return new Response("OK");
    }catch(error){
        return new Response(error, {status:500});
    }
}

addEventListener("fetch", (event) => {
    event.respondWith(handleRequest(event));
});
```

2. Persisting a JSON object:

```js
async function handleRequest(event) {
    try{
        const versionId = "v1.0";
        const storage = Azion.Storage.new(versionId);
        const key = "test";
        const data = JSON.stringify({
            name:"John",
            address:"Abbey Road"
        });
        const buffer = new TextEncoder().encode(data);
        await storage.put(key, buffer);
        return new Response("OK");
    }catch(error){
        return new Response(error, {status:500});
    }
}

addEventListener("fetch", (event) => {
    event.respondWith(handleRequest(event));
});

```

3. Saving a JSON with metadata:

```js
async function handleRequest(event) {
    try{
        const versionId = "v1.0";
        const storage = Azion.Storage.new(versionId);
        const key = "test2";
        const data = JSON.stringify({
            name:"Paul",
            address:"Abbey Road"
        });
        const buffer = new TextEncoder().encode(data);
        const options = { "content-type": "application/json",
                          "metadata": {
                            info:"test info",
                            counter: "1",
                          }}
        await storage.put(key, buffer, options);
        return new Response("OK");
    }catch(error){
        return new Response(error, {status:500});
    }
}

addEventListener("fetch", (event) => {
    event.respondWith(handleRequest(event));
});

```

---

### async Storage.get(key)

the `Storage.get(key)` method is used to retrieve an object.

:::note
The method is async, and must be used with await or event.waitUntil.
:::

#### Syntax 

```js
async Storage.get(key)
```

#### Parameters

| Parameter | Type | Description |
| - | - | - |
| `key` | string | Key to a group of stored objects. If the key doesn't match any existing version ID, a new one is created. |

#### Return 

| Success | Error | 
|-|-|
| Returns an object of the class `StorageObject` | It throws a `StorageError`|


#### Code sample

1. Retrieving content from the storage and returning it:

```js
async function handleRequest(event) {
    try{
        const versionId = "v1.0";
        const storage = Azion.Storage.new(versionId);
        const key = "test";
        const storageObject = await storage.get(key);
        return new Response(storageObject.content);
    }catch(error){
        return new Response(error, {status:500});
    }
}


addEventListener("fetch", (event) => {
    event.respondWith(handleRequest(event));
});
```

2. Getting a JSON from the storage:

```js
async function handleRequest(event) {
    try{
        const versionId = "v1.0";
        const storage = Azion.Storage.new(versionId);
        const key = "test";
        const storageObject = await storage.get(key); 
        const data = new TextDecoder().decode(await storageObject.arrayBuffer());
        return new Response(data);
    }catch(error){
        return new Response(error, {status:500});
    }
}

addEventListener("fetch", (event) => {
    event.respondWith(handleRequest(event));
});
```

3. Reading an object's metadata:

```js
async function handleRequest(event) {
    try{
        const versionId = "v1.0";
        const storage = Azion.Storage.new(versionId);
        const key = "test2"
        const storageObject = await storage.get(key);
        return new Response(storageObject.metadata.get("info"));   
    }catch(error){
        return new Response(error, {status:500});
    }
}

addEventListener("fetch", (event) => {
    event.respondWith(handleRequest(event));
});
``` 

---

### async Storage.delete(key)

the `Storage.get(key)` method is used to retrieve an object.

:::note
The method is async, and must be used with await or event.waitUntil.
:::

#### Syntax 

The `Storage.delete(key)` is used to remove an object from Azion Storage.
```js
async Storage.delete(key)
```

#### Parameters

| Parameter | Type | Description |
| - | - | - |


| `key` | string | Key to a group of stored objects. If the key doesn't match any existing version ID, a new one is created. |

#### Return 

| Success | Error | 
|-|-|
| Returns an object of the class `StorageObjectList` | It throws a `StorageError`|


#### Code sample

1. Listing objects stored in Azion Storage related to a specific `versionId`:

```js
async function handleRequest(event) {
    try{
        const versionId = "v1.0";
        const storage = Azion.Storage.new(versionId);
        const objectsList = await storage.list();
        for (const entry of objectsList.entries) {
            console.log(`key: ${entry.key} length: ${entry.content_length}`);
        }
        return new Response("Ok");   
    }catch(error){
        return new Response(error, {status:500});
    }
}

addEventListener("fetch", (event) => {
    event.respondWith(handleRequest(event));
});

```

---

### async Storage.list()

the `Storage.list()` method is used to list all objects belonging to the specif `versionId`.

:::note
The method is async, and must be used with await or event.waitUntil.
:::

#### Syntax 

The `Storage.delete(key)` is used to remove an object from Azion Storage.
```js
await storage.list()
```

#### Parameters

| Parameter | Type | Description |
| - | - | - |
| `key` | string | Key to a group of stored objects. If the key doesn't match any existing version ID, a new one is created. |

#### Return 

| Success | Error | 
|-|-|
| No response | It throws a `StorageError`|


#### Code sample

1. Removing an object from Azion Storage:

```js
async function handleRequest(event) {
    const versionId = "v1.0";
    const storage = Azion.Storage.new(versionId);
    const key = "test";
    try{
        await storage.delete(key);
    }catch(error){
        return new Response(error, {status:500});
    }
    return new Response("Ok");
}

addEventListener("fetch", (event) => {
    event.respondWith(handleRequest(event));
});

```

---

### StorageObject Class Methods

|Method|Description|
|-|-|
|`StorageObject.content`|Read-only property containing a ReadableStream for the content stored in the storage.|
|`async StorageObject.arrayBuffer()`| Asynchronous function that returns an ArrayBuffer with the content stored in the storage. This method consumes the ReadableStream from the content property.|
|`StorageObject.metadata`| Read-only property containing a Map object (https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) with the metadata of the object stored in the storage.|
| `StorageObject.contentType`|Read-only property containing the content-type of the content stored in the storage.|
| `StorageObject.contentLength`|  Read-only property containing the size in bytes of the content stored in the storage.|