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

## Methods 

### Storage.put

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