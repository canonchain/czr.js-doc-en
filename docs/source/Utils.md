# Utils

## toBigNumber

Convert a value to `bignumber`

```
czr.utils.toBigNumber(value)
```

### Parameters

| Field  | Type            | Description         |
| ----- | --------------- | ------------ |
| value | String / Number | Value to convert |

### Results

A value in Bignumber type.

```
BigNumber { s: 1, e: 0, c: [ 2 ] }
```

### Example

```
const bigVal = czr.utils.toBigNumber(2);
```

## isBigNumber

Check if the value is a `bignumber` type.

```
czr.utils.isBigNumber(value)
```

### Parameters

| Field  | Type             | Description        |
| ----- | ----------------- | ------------ |
| value | String / Number /Bignumber ... | Value to check |

### Results

If the value is in Bignumber type，return `true`. Otherwise, return `false`.

### Example

```
const isBig = czr.utils.isBigNumber(2);
```

## encode

Encode an object.

```
czr.utils.encode.parse(parm);
```

### Parameters

| Field | Type   | Description   |
| ---- | ------ | -------------- |
| parm | Object | The object to be encoded. |

### Returns

Encoded bytecode.

### Example

```
let parm = {
    functionName: "constructor",
    args: ["1000000000000000000000000000", "canonChain", "CZR"]
};
let data = czr.utils.encode.parse(parm);

console.log("********************* data **********************");
console.log(data);

// Returns
//{ functionName: 'constructor',
  args: [ '1000000000000000000000000000', 'canonChain', 'CZR' ],
  funABI:
   { inputs: [ [Object], [Object], [Object] ],
     payable: false,
     stateMutability: 'nonpayable',
     type: 'constructor' },
  data:
   '60806040...' }
```

## decode

Decode a bytecode according to an ABI.

```
utils.decode.parse(bytecode, abi);
```

### Parameters

| Field    | Type         | Description           |
| -------- | ------------ | --------------------- |
| bytecode | Hexdecimal   | data to be decoded    |
| abi      | JSON         | decode format         |

### Result

Decoded object.

### Example

```
let abi = {
    constant: true,
    inputs: [],
    name: "name",
    outputs: [{ name: "", type: "string" }],
    payable: false,
    stateMutability: "view",
    type: "function",
}

let name_response = "0x" + "0000000000000000000000000000000000000000000000000000000000000020000000000000000000000000000000000000000000000000000000000000000A63616E6F6E436861696E00000000000000000000000000000000000000000000";

let nameInfo2 = czr.utils.decode.parse(name_response, abi);
//[ { name: '', type: 'string', value: 'canonChain' } ]
```

## encodeAccount

Convert a hexdecimal value to a Canonchain account address in `czr_xxx` format.

```
czr.utils.encodeAccount(value);
```

### Parameters

| Field  | Type        | Description       |
| ----- | ------------ | ------------ |
| value | Hexdecimal   | Value to be converted. |

### Returns

Canonchain account address in `czr_xxx` format.

### Example

```
let czrAcc = czr.utils.encodeAccount("B5F327E3F07F2C94DADCDB6D122ADDAFD3AA3AC9507E8F8368F9AD3E6A378798")
console.log(czrAcc);//czr_4KsqkcZCs6i9VU2WUsiqTU8M6i3WYpVPFMcMXSkKmB92GJvYt1
```

## decodeAccount

Convert a Canonchan account address in `czr_xxx` format to hexdecimal value.

```
czr.utils.decodeAccount(value);
```

### Parameters

| Field | Type           | Description        |
| ----- | -------------- | ------------ |
| value | Canonchain account address | Value to be converted. |

### Results

Hexdecimal value

### Example

```
try {
    let acc = czr.utils.decodeAccount('czr_4KsqkcZCs6i9VU2WUsiqTU8M6i3WYpVPFMcMXSkKmB92GJvYt1');
    console.log(acc)
} catch (error) {
    console.log(error)
}
```

## fromCan

Convert an amount of tokens in uint of `can` to an equivalent amount in unit of `czr`.

```
czr.utils.fromCan(czrVal)
```

### Parameters

| Field   | Type   | Description         |
| ------ | ------ | ------------ |
| czrVal | Number | Amount to be converted |

### Result

Amount in the uint of `czr`.

### Example

```
let val = czr.utils.fromCan(2);//0.000000000000000002
```

## fromCanToken

Convert an amount of tokens in uint of `can` to an equivalent amount in specific precision.

```
czr.utils.fromCan(value,precision)
```

### Parameters

| Field     | Type          | Description                 |
| --------- | ------------- | --------------------------- |
| value     | Number/String | Amount to be converted      |
| precision | Number/String | Precision                   |

### Results

Amount in a specific precision.

### Example

```
let val = czr.utils.fromCanToken(2,1000000000000000000);//0.000000000000000002
```

## toCan

Convert an amount of tokens in uint of `czr` to an equivalent amount in unit of `can`.

```
czr.utils.toCan(value)
```

### Parameters

| Field | Type   | Description         |
| ----- | ------ | ------------ |
| value | Number | Value to be converted |

### Results

Amount in the uint of `can`.

### Example

```
let val = czr.utils.toCan(2);//2000000000000000000
```
