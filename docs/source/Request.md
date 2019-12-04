# RPC requests

## accountBalance

Get the balance of an account.
```
request.accountBalance
```

### Parameters

| Field    | Type   | Description       |
|---------|--------|------------|
| account | string | account address |

### Returns

| Field    | Type   | Description     |
|---------|--------|----------|
| code    | string | -        |
| msg     | string | -        |
| balance | string | Account balance |

**Error code**

| Name | Description                      |
|------|---------------------------|
| 1    | Invalid account           |
| 100  | Missing parameter         |



## accountBlockList

Get the list of blocks from an account.

Note：set `rpc_control` to be `true` when the node starts

```
request.accountBlockList
```

### Parameters

| Field         | Type   | Description                                                |
|--------------|--------|-----------------------------------------------------|
| account      | string | Account address                                        |
| limit `Optional` | string | Uplimit of number of blocks to return. The default value is 1000          |
| index `Optional` | string | Index to start from，which should be derived from next_index field from last returns. The default value is empty.|

### Returns

| Field       | Type   | Description         |
|------------|--------|--------------|
| code       | string | -            |
| msg        | string | -            |
| blocks     | string | list of blocks |
| next_index | string | the next query index |

**Error code**

| Name | Description                                           |
|------|------------------------------------------------|
| 1    | Invalid account                                |
| 2    | Invalid limit                                  |
| 3    | Limit too large, it can not be large than 1000 |
| 4    | Invalid index                                  |
| 5    | Index not found                                |
| 100  | Missing parameter.                             |



## accountChangePwd

Change the account password.

Note：set `rpc_control` to be `true` when the node starts

```
request.accountChangePwd
```

### Parameters

| Field    | Type   | Description           |
|---------|--------|----------------|
| account | string | Account address |
| oldPwd  | string | Original password     |
| newPwd  | string | New password     |

### Returns

| Field  | Type   | Description                                   |
|-------|--------|----------------------------------------|
| code  | string | -                                      |
| msg   | string | -                                      |
| valid | string | Password validation result，0: Invalid format，1: Valid format. |

**Error code**

| Name | Description                                                                                                                                     |
|------|------------------------------------------------------------------------------------------------------------------------------------------|
| 1    | Invalid account                                                                                                                          |
| 2    | Account not found                                                                                                                        |
| 3    | Invalid new password! A valid password length must between 8 and 100                                                                     |
| 4    | Invalid new password! A valid password must contain characters from letters (a-Z, A-Z), digits (0-9) and special characters (!@#\$%^&\*) |
| 5    | Wrong old password                                                                                                                       |
| 100  | Missing parameter                                                                                                                        |



## accountCode

Get code from an account if it is a contract account.

```
request.accountCode
```

### Parameters

| Field    | Type   | Description           |
|---------|--------|----------------|
| account | string | Contract account |

### Returns

| Field | Type   | Description |
|------|--------|------|
| msg  | string | -    |
| code | string | -    |

**Error code**

| Name | Description            |
|------|-----------------|
| 1    | Invalid account |



## accountCreate

Create an account.

Note：set `rpc_control` to be `true` when the node starts

```
request.accountCreate
```

### Parameters

| Field                 | Type   | Description                                                                         
|----------------------|--------|---------------------|
| pwd                  | string | Account password                                                              

### Returns

| Field | Type   | Description                        |
|------|--------|-----------------------------|
| code | string | 0 if Success |
| msg  | string | ok if Success |

**Error code**

| Name | Description                                                                                                                                 |
|------|--------------------------------------------------------------------------------------------------------------------------------------|
| 1    | Password can not be empty                                                                                                            |
| 2    | Invalid password! A valid password length must between 8 and 100                                                                     |
| 3    | Invalid password! A valid password must contain characters from letters (a-Z, A-Z), digits (0-9) and special characters (!@#\$%^&\*) |
| 100  | Missing parameter pwd                                                                                                                |



## accountExport

Export an account

```
request.accountExport
```

### Parameters

| Field    | Type   | Description       |
|---------|--------|------------|
| account | string | Account |

### Returns

| Field | Type   | Description                        |
|------|--------|-----------------------------|
| code | string | Error code|
| msg  | string | Error message |
| json | object | Exported account json object |

**Error code**

| Name | Description              |
|------|-------------------|
| 1    | Invalid account   |
| 2    | Account not found |


## accountImport

Import an account

Note：set `rpc_control` to be `true` when the node starts

```
request.accountImport
```

### Parameters

| Field                 | Type   | Description                                                                         |
|----------------------|--------|---------------------|
| jsonFile             | object | Import account json file                                                             

### Returns

| Field    | Type   | Description                        |
|---------|--------|-----------------------------|
| code    | string | If success，code returns 0|
| msg     | string | Error message |
| account | string | Imported account           |

**Error code**

| Name | Description                       |
|------|----------------------------|
| 1    | Invalid account            |
| 2    | Invalid json               |
| 100  | Missing parameter jsonFile |

## accountList

```
request.accountList
```

### Returns

| Field     | Type   | Description                          |
|----------|--------|-------------------------------|
| code     | string | -                             |
| msg      | string | -                             |
| accounts | object | accounts: {string[]} list of accounts|

## accountLock

Lock an account

Note：set `rpc_control` to be `true` when the node starts

```
request.accountLock
```

### Parameters

| Field    | Type   | Description       |
|---------|--------|------------|
| account | string | Account to lock|
| pwd     | string | Account password       |

### Returns

| Field | Type   | Description                        |
|------|--------|-----------------------------|
| code | string | Error code|
| msg  | string | Error message |

**Error code**

| Name | Description              |
|------|-------------------|
| 1    | Invalid account   |
| 2    | Account not found |
| 100  | Missing parameter |


## accountRemove

Remove an account.

Note：set `rpc_control` to be `true` when the node starts

```
request.accountRemove
```

### Parameters

| Field    | Type   | Description       |
|---------|--------|------------|
| account | string | Account to remove |
| pwd     | string | Account password       |

### Returns

| Field | Type   | Description                        |
|------|--------|-----------------------------|
| code | string | Error code|
| msg  | string | Error message |

**Error code**

| Name | Description              |
|------|-------------------|
| 1    | Invalid account   |
| 2    | Account not found |
| 3    | Wrong password    |
| 100  | Missing parameter |



## accountUnlock

Unlock an account

Note：set `rpc_control` to be `true` when the node starts.

```
request.accountUnlock
```

### Parameters

| Field    | Type   | Description       |
|---------|--------|------------|
| account | string | Account to unlock |
| pwd     | string | Account password       |

### Returns

| Field | Type   | Description                        |
|------|--------|-----------------------------|
| code | string | Error code|
| msg  | string | Error message |

**Error code**

| Name | Description              |
|------|-------------------|
| 1    | Invalid account   |
| 2    | Account not found |
| 3    | Wrong password    |
| 100  | Missing parameter |


## accountValidate

Validate account format

```
request.accountValidate
```

### Parameters

| Field       | Type   | Description            |
|------------|--------|---------------------|
| accountVal | string | Account to validate |

### Returns

| Field  | Type   | Description                               |
|-------|--------|----------------------------------------|
| code | string | Error code|
| msg  | string | Error message |
| valid | string | Validation result，0: Invalid，1: Valid.   |


## accountsBalances

Check balance for multiple accounts

```
request.accountsBalances
```

### Parameters

| Field    | Type  | Description          |
|---------|-------|-------------------|
| account | Array | Array of accounts |

### Returns

| Field     | Type   | Description                           |
|----------|--------|------------------------------------|
| code | string | Error code|
| msg  | string | Error message |
| balances | Object | balances {Object.<string, string>} |

**Error code**

| Name | Description                 |
|------|---------------------------|
| 1    | Invalid account           |
| 100  | Missing parameter account |


## call

Get contract states

```
request.call
```

### Parameters

| Field        | Type   | Description                                                             |
|-------------|--------|----------------------------------------------------------------------|
| from `Optional` | string | Sender account                                                     |
| to            | string | Receiver account                                                   |
| data `Optional` | string | Contract data or code                                              |
| mci `Optional`  | string | mci，acceptable value: "latest", "earliest" or string of digits（e.g: "1352"）. The default value is "latest" |

### Returns

| Field | Type   | Description |
|------|--------|------|
| code | string | Error code|
| msg  | string | Error message |

**Error code**

| Name | Description                   |
|------|------------------------|
| 1    | Invalid from account   |
| 2    | From account not found |
| 3    | Invalid to account     |
| 4    | Invalid data format    |
| 5    | Data size too large    |
| 6    | Invalid mci format     |
| 100  | Missing parameter      |



## estimateGas

estimate gas consumption for a transaction

```
request.estimateGas
```

### Parameters

| Field             | Type   | Description                                                                             |
|------------------|--------|----------------------------------------------------------------------------------|
| from `Optional`      | string | Sender account                                                                       |
| to `Optional`        | string | Receiver account                                                                  |
| amount `Optional`    | string | Amount, unit: 1\*10<sup>-18</sup>CZR                                               |
| gas `Optional`       | string | Gas uplimit for the transaction                                                         |
| gas_price `Optional` | string | Gas price，unit: 1\*10<sup>-18</sup>CZR/gas，gas fee = actual gas consumption * gas_price |
| data `Optional`      | string | Contract code or data. The default value is empty.                                                     |
| mci `Optional`       | string | mci，acceptable value: "latest", "earliest" or string of digits（e.g: "1352"）. The default value is "latest"        |

### Returns

| Field | Type   | Description               |
|------|--------|--------------------|
| code | string | Error code|
| msg  | string | Error message |
| gas  | string | Estimated gas for the transaction |

**Error code**

| Name | Description                           |
|------|--------------------------------|
| 1    | Invalid from account           |
| 2    | Invalid to account             |
| 3    | Invalid amount format          |
| 4    | Invalid gas format             |
| 5    | Invalid data format            |
| 6    | Data size too large            |
| 7    | Invalid gas price format       |
| 8    | Invalid mci format             |
| 9    | IGas not enough or excute fail |
| 100  | Missing parameter              |



## generateOfflineBlock

Generate an unsigned block.

Note：set `rpc_control` to be `true` when the node starts.

```
request.generateOfflineBlock
```

### Parameters

| Field            | Type   | Description                                                                             |
|-----------------|--------|----------------------------------------------------------------------------------|
| previous `Optional` | string | Specify the last block hash of the sender’s account. It could be used to skip the blocks in the account that are not referenced by any witnesses.                               |
| from            | string | Sender account                                                                          |
| to              | string | Receiver account                                                                  |
| amount          | string | Amount，unit: 1\*10<sup>-18</sup>CZR                                               |
| gas             | string | Gas uplimit for the transaction. Unused gas fee will be returned to the sender account.                              |
| gas_price       | string | Gas price，unit: 1\*10<sup>-18</sup>CZR/gas，gas fee = actual gas consumption * gas_price |
| data `Optional`     | string | Contract code or data. The default value is empty.                       |

### Returns

| Field            | Type   | Description                                                                             |
|-----------------|--------|----------------------------------------------------------------------------------|
| code | string | Error code|
| msg  | string | Error message |                                                                              
| hash            | string | block hash     |                                                               
| previous `Optional` | string | the last block of the sender account |    
| from            | string | Sender account                                                   |
| to              | string | Receiver account                                                                  |
| amount          | string | Amount，unit: 1\*10<sup>-18</sup>CZR                             |
| gas             | string | Gas uplimit for the transaction. Unused gas fee returns to the sender account. |
| gas_price       | string | Gas price，unit: 1\*10<sup>-18</sup>CZR/gas，gas fee = actual gas consumption * gas_price |

**Error code**

| Name | Description                          |
|------|-------------------------------|
| 1    | Invalid from account          |
| 3    | Invalid to account            |
| 4    | Invalid amount format         |
| 5    | Invalid gas format            |
| 6    | Invalid data format           |
| 7    | Data size too large           |
| 8    | Insufficient balance          |
| 9    | Validate error                |
| 10   | Compose error                 |
| 100  | Missing parameter transaction |
| 110  | transaction not valid         |


## getBlock

Get content of a block.

```
request.getBlock
```

### Parameters

| Field  | Type  | Description                                 |
|-------|-------|------------------------------------------|
| hashs | Array | Block hash                               |

### Returns

| Field   | Type   | Description     |
|--------|--------|----------|
| code | string   | Error code|
| msg  | string   | Error message | 
| blocks | Array  | Content of blocks. Return null if hash doesn't exist|

**Error code**

| Name | Description           |
|------|---------------------|
| 1    | Invalid hash format |



## getBlockState

Get state of a block.

```
request.getBlockState
```

### Parameters

| Field | Type   | Description     |
|------|--------|----------|
| hash | string | Block hash |

### Returns

| Field        | Type   | Description                                                                                                                       |
|-------------|--------|--------------------------------|
| code | string   | Error code|
| msg  | string   | Error message | 
| block_state | object | See block state in the [block_state RPC method](https://canonchain.readthedocs.io/en/latest/source/JSON-RPC-Interfaces.html#block_state). If the block hash doesn’t exist, this object is null.|

**Error code**

| Name | Description           |
|------|---------------------|
| 1    | Invalid hash format |


## getBlockStates

Get block states in batch.

```
request.getBlockStates
```

### Parameters

| Field  | Type  | Description     |
|-------|-------|----------|
| hashs | Array | Array of block hashes |

### Returns

| Field         | Type   | Description                                                                                                                       |
|--------------|--------|-------------------------------------|
| code | string   | Error code|
| msg  | string   | Error message | 
| block_states | Array  | List of block states. See block state in the [block_state RPC method](https://canonchain.readthedocs.io/en/latest/source/JSON-RPC-Interfaces.html#block_state). If any of the block hashes doesn’t exist, the corresponding list element is null. |

**Error code**

| Name | Description           |
|------|---------------------|
| 1    | Invalid hash format |



## logs

The event logs of smart contract execution.

```
request.logs(obj)
```

### Parameters

| Field       | Type   | Description                                             |
|------------|--------|--------------------------------------------------|
| obj `Optional` | Object | `from_stable_block_index` / `account` / `topics` |


### Returns

| Field | Type   | Description |
|------|--------|------|
| code | string   | Error code |
| msg  | string   | Error message | 
| logs | Array  | Array of logs |

```
// Success
{
    "code": 0,
    "msg": "OK",
    "logs": [
        {
            "address": "czr_3DG8FjYSAqkBNubcSVAAjAtSQ9Q2tWVNwPS8VHQ55XwWG4DsTS",
            "data": "0000000000000000000000000000000000000000000000000000000000000000",
            "topics": [
                "260823607ceaa047acab9fe3a73ef2c00e2c41cb01186adc4252406a47d73446"
            ]
        },
        {
            "address": "czr_3DG8FjYSAqkBNubcSVAAjAtSQ9Q2tWVNwPS8VHQ55XwWG4DsTS",
            "data": "0000000000000000000000000000000000000000000000000000000000000001",
            "topics": [
                "260823607ceaa047acab9fe3a73ef2c00e2c41cb01186adc4252406a47d73446"
            ]
        }
    ]
}

// Failed
{
    "code": 3,
    "msg": "Invalid account"
}
```

## sendBlock

Send a block.

Note：set `rpc_control` to be `true` when the node starts.

```
request.sendBlock
```

### Parameters

| Field            | Type   | Description                                                                             |
|-----------------|--------|----------------------------------------------------------------------------------|
| previous `Optional` | string | Specify the last block hash of the sender account. It could be used to skip the blocks in the account that are not referenced by any witnesses.           |
| from            | string | Sender account             |
| to              | string | Receiver account           |
| amount          | string | Amount, unit: 1\*10<sup>-18</sup> CZR  |
| password        | string | Sender account password    |
| gas             | string | Gas uplimit for the block. Unused gas fee will be returned to the sender account. |
| gas_price       | string | Gas price，unit: 1*10<sup>-18</sup>CZR/gas，gas fee = actual gas consumption * gas_price |
| data `Optional`     | string | Contract code or data. The default value is empty. |

### Returns

| Field | Type   | Description      |
|------|--------|-----------|
| code | string   | Error code |
| msg  | string   | Error message |
| hash | string   | block hash |

**Error code**

| Name | Description                          |
|------|-------------------------------|
| 1    | Invalid from account          |
| 2    | From account not found        |
| 3    | Invalid to account            |
| 4    | Invalid amount format         |
| 5    | Invalid gas format            |
| 6    | Invalid data format           |
| 7    | Data size too large           |
| 9    | Account locked                |
| 10   | Wrong password                |
| 11   | Insufficient balance          |
| 100  | Missing parameter transaction |
| 110  | transaction not valid         |



## sendOfflineBlock

Send a signed block. The parameters are derived from [generateOfflineBlock](#generateOfflineBlock) return fields. Returns the block hash.

Note：set `rpc_control` to be `true` when the node starts.

```
request.sendOfflineBlock
```

### Parameters

| Field            | Type   | Description                                                                             |
|-----------------|--------|----------------------------------------------------------------------------------|
| previous `Optional` | string | Specify the last block hash of the sender account. It could be used to skip the blocks in the account that are not referenced by any witnesses.           |
| from            | string | Sender account             |
| to              | string | Receiver account           |
| amount          | string | Amount, unit: 1\*10<sup>-18</sup> CZR. |
| gas             | string | Gas uplimit for the block. Unused gas fee will be returned to the sender account. |
| gas_price       | string | Gas price，unit: 1*10<sup>-18</sup>CZR/gas，gas fee = actual gas consumption * gas_price |
| data `Optional`     | string | Contract code or data. The default value is empty. | 
| signature       | string | Signature of the block. |

### Returns

| Field  | Type     | Description   |
|-------|---------|------------|
| code | string   | Error code |
| msg  | string   | Error message |
| hash | string   | block hash |

**Error code**

| Name | Description                     |
|------|--------------------------|
| 1    | Invalid from account     |
| 3    | Invalid to account       |
| 4    | Invalid amount format    |
| 5    | Invalid gas format       |
| 6    | Invalid data format      |
| 7    | Data size too large      |
| 9    | Invalid previous format  |
| 12   | Invalid signature format |
| 100  | Missing parameter        |
| 110  | block not valid          |


## signMsg

Sign a message

```
request.signMsg
```

### Parameters

| Field       | Type   | Description       |
|------------|--------|------------|
| public_key | string | Public key of the signature  |
| password   | string | Public key password          |
| msg        | string | Message to be signed         |

### Returns

| Field      | Type   | Description      |
|-----------|--------|-----------|
| code | string   | Error code |
| msg  | string   | Error message |
| signature | string | Signature  |

**Error code**

| Name | Description                      |
|------|---------------------------|
| 1    | Invalid public key format |
| 2    | Invalid msg format        |
| 3    | Wrong password            |
| 100  | Missing parameter         |


## stableBlocks

Retrieve the stabled blocks for a specific mci value.

```
request.stableBlocks
```

### Parameters

| Field         | Type   | Description                                                            |
|--------------|--------|-----------------------------------------------------------------|
| limit        | number | uplimit of the number of blocks returned. Maximum value is 1000. |
| index `Optional` | string | the index of the first block to retrieve. It can be set to be the value of next_index from the result of previous stable_blocks call. The default value is 0. |

### Returns

| Field       | Type   | Description                                                |
|------------|--------|-----------------------------------------------------|
| code | string   | Error code |
| msg  | string   | Error message |
| blocks     | Array  | Array of blocks                                    |
| next_index | number | The stable index for next block. This value is null if there is no subsequent blocks. |

**Error code**

| Name | Description                                      |
|------|------------------------------------------------|
| 1    | Invalid index format                           |
| 2    | Invalid limit format                           |
| 3    | Limit too large, it can not be large than 1000 |



## status

Retrieve the current status of DAG on the node

```
request.status
```

### Returns

| Field                    | Type   | Description                                                                                   |
|-------------------------|--------|------|
| code | string   | Error code |
| msg  | string   | Error message |
| syncing                 | number |  if the node is syncing to the other nodes，0：not syncing，1：syncing.   |
| last_mci                | number | the mci of the last block on the main chain. |
| last_stable_block_index | number | the stable index of the last stable block. stable index starts from value 0 and keep increasing. It indicates the order of stable blocks on DAG. |

## version

Acquire the current node version, rpc interface version, and database version.

```
request.version
```

### Returns

| Field          | Type   | Description |
|---------------|--------|------|
| code | string   | Error code |
| msg  | string   | Error message |
| version       | string | Canonchain node version  |
| rpc_version   | string | RPC interface version    |
| store_version | string | Database version         |



## witnessList

Retrieve the list of witnesses.

```
request.witnessList
```

### Returns

| Field         | Type   | Description       |
|--------------|--------|------------|
| code | string   | Error code |
| msg  | string   | Error message |
| witness_list | Array  | list of witnesses. |


