# Worker Scripts Documentation

## Key Vault (`.get` single key)

To get the value of a key, call the `get()` method. The key vault needs to be bound to the script via namespace.

```javascript
env.NAMESPACE.get(key);
env.NAMESPACE.get('first-key');
```

The `get()` method returns a `promise`.

The promise resolves to a string. If the key is not found, the promise will resolve with the literal value `null`.

## Key Vault (`.get` array of keys)

To get the value of an array of keys, call the `get()` method.

```javascript
env.NAMESPACE.get(keys);
env.NAMESPACE.get(['first-key', 'second-key'];
```

The `get()` method returns a `promise`.

The promise resolves to a Map of the key-value pairs found. Keys not found will have the literal value `null`.
