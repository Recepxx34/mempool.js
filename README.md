# Mempool JS API

[![npm version](https://img.shields.io/npm/v/@mempool/mempool.js.svg?style=flat-square)](https://www.npmjs.org/package/@mempool/mempool.js)
[![NPM](https://img.shields.io/david/mempool/mempool.js.svg?style=flat-square)](https://david-dm.org/mempool/mempool.js#info=dependencies)
[![Known Vulnerabilities](https://snyk.io/test/github/mempool/mempool.js/badge.svg?style=flat-square)](https://snyk.io/test/github/mempool/mempool.js)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg?style=flat-square)](https://opensource.org/licenses/MIT)

NPM package module for Mempool APIs.

Documentation: [https://mempool.space/api](https://mempool.space/api)

---

## **Installation**

### **ES Modules**

Install the npm module.

```bash
<!DOCTYPE html>
<html>
  <head>
    <script src="https://mempool.space/mempool.js"></script>
    <script>
      const init = async () => {
        
        const { bitcoin: { websocket } } = mempoolJS({
          hostname: 'mempool.space'
        });

        const ws = websocket.initClient({
          options: ['blocks', 'stats', 'mempool-blocks', 'live-2h-chart'],
        });

        ws.addEventListener('message', function incoming({data}) {
          const res = JSON.parse(data.toString());
          if (res.block) {
            document.getElementById("result-blocks").textContent = JSON.stringify(res.block, undefined, 2);
          }
          if (res.mempoolInfo) {
            document.getElementById("result-mempool-info").textContent = JSON.stringify(res.mempoolInfo, undefined, 2);
          }
          if (res.transactions) {
            document.getElementById("result-transactions").textContent = JSON.stringify(res.transactions, undefined, 2);
          }
          if (res["mempool-blocks"]) {
            document.getElementById("result-mempool-blocks").textContent = JSON.stringify(res["mempool-blocks"], undefined, 2);
          }
        });
  
      };
      init();
    </script>
  </head>
  <body>
    <h2>Blocks</h2><pre id="result-blocks">Waiting for data</pre><br>
    <h2>Mempool Info</h2><pre id="result-mempool-info">Waiting for data</pre><br>
    <h2>Transactions</h2><pre id="result-transactions">Waiting for data</pre><br>
    <h2>Mempool Blocks</h2><pre id="result-mempool-blocks">Waiting for data</pre><br>
  </body>
</html>
```

Or if you're not into package management, just [download a ZIP](https://github.com/mempool/mempool.js/archive/refs/heads/main.zip) file.

Import the module.

```js
import mempoolJS from '@mempool/mempool.js';

// default mempool.space endpointsconst { bitcoin, liquid } = mempoolJS();

// (optional) your custom endpoints
const { bitcoin } = mempoolJS({
  protocol: 'https', // optional, defaults to http for localhost, otherwise https
  hostname: 'mempool.space',
  network: 'testnet' // 'signet' | 'testnet' | 'mainnet',
  config: { // optional axios request config to add to requests
    headers: {
      authorization: 'Basic auth'
    }
  }
});

// Liquid API
const { liquid } = mempoolJS({
  protocol: 'https', // optional, defaults to http for localhost, otherwise https
  hostname: 'liquid.network',
  network: 'liquid' // 'liquid' | 'liquidtestnet'
});
```

### **CommonJS**

Include the line below in the `head` tag of your html file.

```html
<script type="text/javascript" src="https://mempool.space/mempool.js"></script>
```

Call `mempoolJS()` function to access the API methods.

```js
// default mempool.space endpoints
const { bitcoin } = mempoolJS();

// (optional) your custom endpoints
const { bitcoin } = mempoolJS({
  protocol: 'https', // optional, defaults to http for localhost, otherwise https
  hostname: 'mempool.space',
  network: 'testnet', // 'signet' | 'testnet' | 'mainnet'
});

// Liquid API
const { liquid } = mempoolJS({
  protocol: 'https', // optional, defaults to http for localhost, otherwise https
  hostname: 'liquid.network',
  network: 'liquid' // 'liquid' | 'liquidtestnet'
});
```

---

## **Features**

- [Bitcoin](./README-bitcoin.md)
  - [Addresses](./README-bitcoin.md#get-address)
  - [Blocks](./README-bitcoin.md#get-blocks)
  - [Difficulty Adjustment](./README-bitcoin.md#get-difficulty-adjustment)
  - [Fees](./README-bitcoin.md#get-fees)
  - [Lightning](./README-bitcoin.md#get-network-stats)
  - [Mempool](./README-bitcoin.md#get-mempool)
  - [Transactions](./README-bitcoin.md#get-transactions)
  - [Websocket](./README-bitcoin.md#init-websocket)
- [Liquid](./README-liquid.md#get-address)
  - [Addresses](./README-liquid.md#get-address)
  - [Assets](./README-liquid.md#get-address)
  - [Blocks](./README-liquid.md#get-address)
  - [Fees](./README-liquid.md#get-address)
  - [Mempool](./README-liquid.md#get-address)
  - [Transactions](./README-liquid.md#get-address)
  - [Websocket](./README-liquid.md#init-websocket)

---

## **Contributing**

Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change.

---

## **License** [MIT](https://choosealicense.com/licenses/mit/)
