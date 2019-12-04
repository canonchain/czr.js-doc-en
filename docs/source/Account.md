# Accounts

## create

Create a new account.

```
czr.accounts.create(password)
    .then(res => {})
    .catch()
```

### Parameters

| Field    | Type   | Description       |
| -------- | ------ | ---------- |
| password | String | account password |

### Results

keystore file of a new account.

### Example

```
czr.accounts.create(123456).then(res => {
    console.log("Create account result\n", res);//res.account
    console.log(`res.account:${JSON.stringify(res)}`);
}).catch(err => {
    console.log("err===>", err);
});
```

## validateAccount

Validate if the `keystore` file is decodable by the password.

```
czr.accounts.validateAccount(keystore,password)
    .then(res => {})
    .catch()
```

### Parameters

| Field    | Type     | Description      |
| -------- | -------- | ---------- |
| keystore | Keystore | account file   |
| password | String   | account password |

### Results

If the password can decode the `keystore` file, return `true`. Otherwise, return `false`.

### Example

```
czr.accounts.validateAccount(keystore,123456).then(res => {
    console.log("Result\n", res);
}).catch(err => {
    console.log("err===>", err);
});
```

## decrypt

Derive the privateKey from `keystore` file and account password.

```
czr.accounts.decrypt(keystore,password)
    .then(res => {})
    .catch()
```

### Parameters

| Field    | Type     | Description       |
| -------- | -------- | ---------- |
| keystore | Keystore | account file   |
| password | String   | account password |

### Results

If the password can decode `keystore` file, return the privateKey. Otherwse, report error.

### Example

```
czr.accounts.decrypt(keystore,123456).then(res => {
    console.log("Result\n", res);
}).catch(err => {
    console.log("err===>", err);
});
```

## sign

Sign the transaction using privateKey.

```
czr.accounts.sign(transHash,privateKey)
    .then(res => {})
    .catch()
```

### Parameters

| Field       | Type   | Description              |
| ---------- | ------ | ----------------- |
| transHash  | String | hash of transaction to be signed |
| privateKey | String | account privateKey       |

### Returns

Signed transaction

### Example

```
czr.accounts.decrypt(account_keystore, '1234qwer')
    .then(privateKey => {
        console.log('privateKey', privateKey)
        let blockHash='5E844EE4D2E26920F8B0C4B7846929057CFCE48BF40BA269B173648999630053';
        czr.accounts.sign(blockHash, privateKey)
            .then(signature => {
                console.log('signature', signature)
            })
            .catch(console.error)
    })
    .catch(console.error)
```
