# Example

`czr.js` is a library for interacting with canonchain nodes.

## Install

First, you need to put `czr.js` into your project.

You can do this using:

```
npm install czr
```

After that, you need to start the local Canonchain node and instantiate `czr`.

Canonchain download: <http://dev.canonchain.com/download.html>

Canonchain command line: <https://canonchain.readthedocs.io/zh/latest/source/Command-Line-Interfaces.html>

Port used by default `127.0.0.1:8765`

## Use

```js
let Czr = require("czr");
let czr = new Czr();// Use by default 127.0.0.1:8765

// If you want to modify the port, please set the following
// Example
// const options = {
//     host: "127.0.0.1",
//     port: 8888
// };
// let czr = new Czr(options);

//Now you can use the czr object
//Example
czr.request.status().then(function (res) {
    console.log(`status`,res);
}).catch(function(error){
    console.log("accountList catch",error)
});
```