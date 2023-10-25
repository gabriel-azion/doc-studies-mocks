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

To pass the `options` parameter, it's necessary to an object with the following attributes:

| Attribute | Type | Description |
| - | - | - |
| `content-type` | string | O content-type do objeto a ser criado. É similar ao HTTP Header Content-type e descreve como o conteúdo do object storage deve ser tratado. Content-type é opcional, o valor default é application/octet-stream. |
| `content-length` | string | É o tamanho do objeto a ser criado em bytes. É mandatório quando o value é ReadableStream. |
| `metadata` | object | Qualquer objeto javascript contendo informações sobre o objeto que será armazenado no Storage. Todas as properties do objeto devem ser strings. |

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

**StorteObject example**: 

```
Don't know
```

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

**StorageError example**:

```
Don't know
```

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

**StorageError example**:

```
Don't know
```

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

### Métodos da classe StorageObject

|Method|Description|
|-|-|
|`StorageObject.content`|read-only property contendo um ReadbleStream para o conteúdo armazenado no storage.|
|`async StorageObject.arrayBuffer()`| Função assíncrona que retorna um ArrayBuffer com o conteúdo armazenado no storage. Este método consome o ReadableStream da propriedade content.|
|`StorageObject.metadata`| read-only property contendo a objeto Map(https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Map) com os metadados do objeto armazenado no storage.|
| `StorageObject.contentType`|read-only property contendo o content-type do conteúdo armazenado no storage.|
| `StorageObject.contentLength`|  read-only property contendo o tamanho em bytes do conteúdo armazenado no storage.|
