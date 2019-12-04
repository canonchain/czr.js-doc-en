# Abi

## encodeEventSignature

Encodes the event name to its ABI signature, which are the sha3 hash of the event name including input types.

```
czr.abi.encodeEventSignature(eventName);
```

### Parameters

| Field      | Type           | Description                                                                                                                                           |
| --------- | --------------- | ----------------------------------------------------------------------------------------------------------------------------------------------- |
| eventName | String / Object | The event name to encode. or the JSON interface object of the event. If string it has to be in the form event(type,type,...), e.g: myEvent(uint256,uint32[],bytes10,bytes) |

### Returns

String - The ABI signature of the event.

### Example

```
let sign1 = czr.abi.encodeEventSignature('myEvent(uint256,bytes32)');

let opt2 = {
    name: 'myEvent',
    type: 'event',
    inputs: [{
        type: 'uint256',
        name: 'myNumber'
    }, {
        type: 'bytes32',
        name: 'myBytes'
    }]
};
let sign2 = czr.abi.encodeEventSignature(opt2);
```
