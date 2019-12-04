# Contract

## Usage

`Contract` object facilitates the interaction of the developers to the smart contracts on Canonchain.

> The developer has to provide json interface for a contract.

An example of JSON interface for a contract is as the following:

```json
[
	{
		"constant": true,
		"inputs": [],
		"name": "xxx",
		"outputs": [
			{
				"name": "",
				"type": "uint256"
			}
		],
		"payable": false,
		"stateMutability": "view",
		"type": "function"
	},
	...
]
```

### Rules

- The prameters in `[]` is optional. Other pamameters are mandatory.
- The variable `myContract` in this document is a contract object.

---

## Create a contract

Create a contract object（include all the methods defined in JSON interface).

```js
let myContract = new czr.Contract(jsonInterface[, account][, options])
```

### Prameters

- `jsonInterface` \<Object> ：JSON interface
- `account` \<String> ：Contract address
  - it can also be setup later by using `myContract.options.account = 'czr_account'` 
- `options` \<Object>: Optional parameters for `call` and `sendBlock` methods.
  - `from` \<String>: Sender address.
  - `gas_price` \<String> : Gas price, Unit: 1\*10<sup>-18</sup> CZR.
  - `gas` \<String> | \<Number> ：Gas uplimit for the block.
  - `data` \<String> ：Contract data.

### Returns

`Object`：Contract object and all its methods.

### Example

```js
let myContract = new czr.Contract(
    [...],
    'czr_contract_address',
    {
        from: 'czr_account',
        gas_price: '20000000000',
        gas:'2000000',
        data:''
    }
);
```

---

## myContract properties

- options

  - options.account
  - options.jsonInterface

- methods

## options

```js
myContract.options;
```

### Properties

- account \<String>: Contract account.
- jsonInterface \<Array>: JSON interface.
- data \<String>: Contract data. Used for contract deployment.
- from \<String>: Sender account. Null if there is no sender.
- gas_price \<String>: Gas price.
- gas \<String> | \<Number>: Gas limit of the block.

### Example

```js
// get
myContract.options;
> {
    account: 'contract_account',
    jsonInterface: [...],
    from: 'czr_account',
    gas_price: '10000000000000',
    gas: 1000000
}

// set
myContract.options.account = 'contract_account';
myContract.options.from = 'czr_account';
myContract.options.gas_price = '2000000000';
myContract.options.gas = 5000000;
```

---

## options.account

The account to interact with. The contract object is to use this account as the `'to'` value for all transactions.

### Properties

`myContract.options.account` \<String> | \<Null>: The contract account. `null` if not been set yet.

### Example

```js
//get
myContract.options.account;
> 'czr_contract_address'

// set
myContract.options.account = 'czr_contract_address';
```

---

## options.jsonInterface

Contract JSON interface.

### Properties

`myContract.options.jsonInterface` \<Array>：The contract JSON interface

**Contract instance methods will be regenerated if this value is reset**；

### Example

```js
myContract.options.jsonInterface;
> [
    {
        "type":"function",
        "name":"foo",
        "inputs": [{"name":"a","type":"uint256"}],
        "outputs": [{"name":"b","type":"address"}]
    }
]

// set
myContract.options.jsonInterface = [...];
```

---

## myContract.methods properties

`myContract.methods` returns all methods of the contract, where every method will create an object to `call`, `sendBlock` and `encodeABI`.

---

## myContract methods

- clone
- deploy
- methods
  - methods.myMethod.call
  - methods.myMethod.sendBlock
  - methods.myMethod.encodeABI

---

## clone

Clone a contract instance. The cloned instance is completely independent to the original one.

```js
myContract.clone(); // No parameters
```

### Returns

The new contract instance.

### Example

```js
let contract1 = new czr.Contract(abi, account, {gas_price: '12345678', from: fromAddress});

let contract2 = contract1.clone();
contract2.options.account = account2;

(contract1.options.account !== contract2.options.account);
> true
```

---

## deploy

The contract is deployed by calling this method.

```js
myContract.deploy({
  data: '',
  arguments: []
});
```

### Parameters

- `options` \<Object>: Deployment options.
  - `data` \<String>: Contract code.
  - `arguments` \<Array>（Optional) : Contract constructor paramenters in the deployment. 

### Returns

Object:

- `arguments` \<Array>: The parameters passed to the contractor constructor. Their value may have been changed.
- `sendBlock` \<Function>: Deploy the contract to Canonchain.
- `encodeABI` \<Function>: Enocde the contract ABI，i.e. data and arguments.

### Example

**sendBlock**

```js
// sendBlock promise
myContract
  .deploy({
    data: bytecode
  })
  .sendBlock({
    from: 'czr_account',
    gas: 3000000,
    gas_price: '1000000000'
  })
  .then(data => {
    console.log('data', data);
  })
  .catch(function(error) {
    console.log('error', error);
  });

// sendBlock callback
myContract
  .deploy({
    data: bytecode
  })
  .sendBlock(
    {
      from: 'czr_account',
      gas: 3000000,
      gas_price: '1000000000'
    },
    function(error, transactionHash) {
      console.log('error ==> ', error);
      console.log('transactionHash ==> ', transactionHash);
    }
  );

```

**encodeABI**

```js
// encodeABI
myContract.deploy({
    data: '0x12345...',
    arguments: [123, 'My String']
})
    .encodeABI();

> '0x12345...0000012345678765432'

```

---

## methods

```js
myContract.methods.myMethod([param1[, param2[, ...]]])
```

`myMethod` is a method name in JSON interface, and it can be called in the following ways:

- Name: `myContract.methods.myMethod(123)`
- Name with parameters: `myContract.methods['myMethod(uint256)'](123)`
- Signature：`myContract.methods['0x58cf5f10'](123)`

it is allowed to have methods with same name but different types of parameters.

### Parameters

The parameters are from the definition of JSON interface.

### Returns

Object:

- `arguments` \<Array>: The parameters passed to the contractor constructor. Their value may have been changed.
- `call` \<Function>: Call a get method of the contract without sending a blcok.
- `sendBlock` \<Function>: Send a block to Canonchain.
- `encodeABI` \<Function>: Enocde the method ABI.

---

## methods.myMethod.call

`myContract.methods.myMethod([param1[, param2[, ...]]]).call(options[, callback])`

### Parameters

- options \<Object>：Options for call.
  - from \<String>：Sender's account
- callback \<Function>：The first parameter of the callback is error object, and the second parameter of the callback is contract execution result if there is no error.

### Returns

`Promise` object:

```js
//promise
myContract.methods.testCall1().call()
    .then(data => {
        console.log('testCall1 data', data)
    })
    .catch(function (error) {
        console.log('error', error)
    });


//callback
myContract.methods.testCall1().call(function(error, result){
    ...
})
```

---

## methods.myMethod.sendBlock

Send a block to the contract and execute the transaction in block.

### Parameters

- `options` \<Object>: Options for sendBlock.
  - `from` \<String>: The sender account.
  - `gas_price` \<String>: Gas price for the transaction.
  - `gas` \<String>| \<Number>: Gas limit.
  - `value`  `Number | String | BN | BigNumber`: Value in the transaction.
- `callback` \<Function>: The first parameter of the callback is error object, and the second parameter of the callback is contract execution result if there is no error.

### Returns

\<Promise> Return the transaction receipt.

### Example

```js

// promise
myContract.methods.myMethod(123).sendBlock({from: 'czr_account'})
    .then(function(receipt){
        // transaction receipt
    });

// callback
myContract.methods.myMethod(123).sendBlock({from: 'czr_account'}, function(error, transactionHash){
    ...
});

```

---

## methods.myMethod.encodeABI

```js
myContract.methods.myMethod([param1[, param2[, ...]]]).encodeABI()
```

No parameters

### Returns

\<String>：ABI bytecode.

### Example

```js
let encodeABIData = myContract.methods.myMethod(123).encodeABI();
console.log(encodeABIData);
//'0x58cf5f1000000000000000000000000000000000000000000000000000000000000007B'
```

---
