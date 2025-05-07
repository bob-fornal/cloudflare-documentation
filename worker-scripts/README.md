# Worker Scripts Documentation

## Key Vault

> [!WARNING]  
> Actions against the Key Vault via API incur a hit. Each account allows for 1,200 transactions per 5-minute window.

### Read Key-Value Pairs

* [Bindings](#bindings)
* [`get` single key](#function-get-single-key)
* [`get` Map of key-value](#function-get-map-of-key-value)
* [`getWithMetadata` single key](#function-getwithmetadata-single-key)
* [`getWithMetadata` Map of key-object](#function-getwithmetadata-map-of-key-object)

<hr/>

#### Bindings

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

#### FUNCTION: `.get` single key

> To get the value of a key, call the `get()` method. The key vault needs to be bound to the script via namespace.

```javascript
env.NAMESPACE.get(key);
env.NAMESPACE.get('first-key');
```

* The `get()` method returns a `promise`.
* The promise resolves to a string.
* If the key is not found, the promise will resolve with the literal value `null`.

<hr/>

#### FUNCTION: `.get` Map of key-value

> To get the value of an array of keys, call the `get()` method.

> [!NOTE]
> Max: 100 keys.

```javascript
env.NAMESPACE.get(keys);
env.NAMESPACE.get(['first-key', 'second-key'];
```

* The `get()` method returns a `promise`.
* The promise resolves to a Map of the key-value pairs found.
* Keys not found will have the literal value `null`.

<hr/>

#### FUNCTION: `.getWithMetadata` single key

> To to get a single value along with its metadata, call the `getWithMetadata()` method.

```javascript
env.NAMESPACE.getWithMetadata(key);
env.NAMESPACE.getWithMetadata('first-key');
```

* The `getWithMetadata()` method returns a `promise`.
* The promise resolves to an object, `{ value: string, metadata: object }`.
* If the key is not found, the promise will resolve with the literal value `null`.

<hr/>

#### FUNCTION: `.getWithMetadata` Map of key-object

> To get the value of an array of keys, call the `getWithMetadata()` method.

> [!NOTE]
> Max: 100 keys.

```javascript
env.NAMESPACE.getWithMetadata(keys);
env.NAMESPACE.getWithMetadata(['first-key', 'second-key'];
```

* The `getWithMetadata()` method returns a `promise`.
* The promise resolves to a Map of the key-object pairs (`{ value: string, metadata: object }`) found.
* Keys not found will have the literal value `null`.

