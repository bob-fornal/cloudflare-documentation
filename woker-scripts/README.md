# Worker Scripts Documentation

## Key Vault

### Read Key-Value Pairs

* [`get` single key](#function-get-single-key)
* [`get` Map of key-value](#function-get-map-of-key-value)
* [`getWithMetadata` single key](#function-getwithmetadata-single-key)
* [`getWithMetadata` Map of key-object](#function-getwithmetadata-map-of-key-object)

<hr/>
#### Function: `.get` single key

> To get the value of a key, call the `get()` method. The key vault needs to be bound to the script via namespace.

```javascript
env.NAMESPACE.get(key);
env.NAMESPACE.get('first-key');
```

* The `get()` method returns a `promise`.
* The promise resolves to a string. If the key is not found, the promise will resolve with the literal value `null`.

<hr/>
#### Function: `.get` Map of key-value

> To get the value of an array of keys, call the `get()` method.

```javascript
env.NAMESPACE.get(keys);
env.NAMESPACE.get(['first-key', 'second-key'];
```

* The `get()` method returns a `promise`.
* The promise resolves to a Map of the key-value pairs found. Keys not found will have the literal value `null`.

<hr/>
#### Function: `.getWithMetadata` single key

> To to get a single value along with its metadata, call the `getWithMetadata()` method.

```javascript
env.NAMESPACE.getWithMetadata(key);
env.NAMESPACE.getWithMetadata('first-key');
```

* The `getWithMetadata()` method returns a `promise`.
* The promise resolves to an object, `{ value: string, metadata: object }`. If the key is not found, the promise will resolve with the literal value `null`.

<hr/>
#### Function: `.getWithMetadata` Map of key-object

> To get the value of an array of keys, call the `getWithMetadata()` method.

```javascript
env.NAMESPACE.getWithMetadata(keys);
env.NAMESPACE.getWithMetadata(['first-key', 'second-key'];
```

* The `getWithMetadata()` method returns a `promise`.
* The promise resolves to a Map of the key-object pairs (`{ value: string, metadata: object }`) found. Keys not found will have the literal value `null`.
