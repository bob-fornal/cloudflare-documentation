# Key Vault

> [!WARNING]  
> Actions against the Key Vault via API incur a hit. Each account allows for 1,200 transactions per 5-minute window.

> Due to the eventually consistent nature of the **Key Vault** in Cloudflare, concurrent writes to the same key can end up overwriting one another. It is a common pattern to write data from a single process. This avoids competing concurrent writes because of the single stream. All data is still readily available within all Workers bound to the namespace.

> If concurrent writes are made to the same key, the last write will take precedence.

> [!WARNING]  
> Writes are immediately visible to other requests in the same global network location, but can take up to 60 seconds to be visible in other parts of the world.

## Limits

| Feature | Free | Paid |
|---------|------|------|
| Reads | 100,000 reads per day | Unlimited |
| Writes to different keys | 1,000 writes per day | Unlimited |
| Writes to same key | 1 per second | 1 per second |
| Operations/Worker invocation | 1,000 | 1,000 |
| Namespaces | 1,000 | 1,000 |
| Storage/account | 1 GB | Unlimited |
| Storage/namespace | 1 GB | Unlimited |
| Keys/namespace | Unlimited | Unlimited |
| **Key size** | 512 bytes | 512 bytes |
| **Key metadata** | 1024 bytes | 1024 bytes |
| **Value size** | 25 MiB | 25 MiB |
| Minimum cacheTtl | 60 seconds | 60 seconds |

## Documentation

* [Read Key-Value Pairs](#read-key-value-pairs)
* [Write Key-Value Pairs](#write-key-value-pairs)

## Read Key-Value Pairs

* [Bindings](#bindings)
* [`get` single key](#function-get-single-key)
* [`get` Map of key-value](#function-get-map-of-key-value)
* [`getWithMetadata` single key](#function-getwithmetadata-single-key)
* [`getWithMetadata` Map of key-object](#function-getwithmetadata-map-of-key-object)

<hr/>

### Bindings

KV bindings allow for communication between a Worker and a KV namespace.

The name of a binding does not need to match the KV namespace's name. Instead, the binding should be a valid JavaScript identifier, because the identifier will exist as a global variable within a Worker.

To bind the namespace to your Worker in the Cloudflare dashboard:

1. Log in to the Cloudflare dashboard.
2. Go to Workers & Pages.
3. Select your Worker.
4. Select Settings > Bindings.
5. Select Add.
6. Select KV Namespace.
7. Enter your desired variable name (the name of the binding).
8. Select the KV namespace you wish to bind the Worker to.
9. Select Deploy.

<hr/>

### FUNCTION: `.get` single key

> To get the value of a key, call the `get()` method. The key vault needs to be bound to the script via namespace.

```javascript
env.NAMESPACE.get(key);
env.NAMESPACE.get('first-key');
```

* The `get()` method returns a `Promise`.
* The promise resolves to a string.
* If the key is not found, the promise will resolve with the literal value `null`.

<hr/>

### FUNCTION: `.get` Map of key-value

> To get the value of an array of keys, call the `get()` method.

> [!NOTE]
> Max: 100 keys.

```javascript
env.NAMESPACE.get(keys);
env.NAMESPACE.get(['first-key', 'second-key'];
```

* The `get()` method returns a `Promise`.
* The promise resolves to a Map of the key-value pairs found.
* Keys not found will have the literal value `null`.

<hr/>

### FUNCTION: `.getWithMetadata` single key

> To to get a single value along with its metadata, call the `getWithMetadata()` method.

```javascript
env.NAMESPACE.getWithMetadata(key);
env.NAMESPACE.getWithMetadata('first-key');
```

* The `getWithMetadata()` method returns a `Promise`.
* The promise resolves to an object, `{ value: string, metadata: object }`.
* If the key is not found, the promise will resolve with the literal value `null`.

<hr/>

### FUNCTION: `.getWithMetadata` Map of key-object

> To get the value of an array of keys, call the `getWithMetadata()` method.

> [!NOTE]
> Max: 100 keys.

```javascript
env.NAMESPACE.getWithMetadata(keys);
env.NAMESPACE.getWithMetadata(['first-key', 'second-key'];
```

* The `getWithMetadata()` method returns a `Promise`.
* The promise resolves to a Map of the key-object pairs (`{ value: string, metadata: object }`) found.
* Keys not found will have the literal value `null`.

## Write Key Value Pairs

### FUNCTION `.put` single key-value pair

To create a new key-value pair, or to update the value for a particular key, call the `put()` method.

```javascript
env.NAMESPACE.put(key, value, [options]);
```

Parameters

* Key: string
* Value: string (general use)
* Options: { metadata?: object }

Notes

* The `put()` method returns a `Promise`.
* `await` the `Promise` to verify a successful update.

#### Write data in bulk

> The bulk API can accept up to 10,000 KV pairs at once.

* A key and a value are required for each KV pair.
* The entire request size must be less than 100 megabytes.
* Bulk writes are not supported using the KV binding.
