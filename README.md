# Documentation of the new GasFree functionality from Tron

v 1.1

<!doctype html>
<html lang="ru">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>GasFree Developer Documentation</title>
  <!-- Подключение Google Fonts -->
  <link href="https://fonts.googleapis.com/css?family=Open+Sans:400,600,700&display=swap" rel="stylesheet">
  <!-- Встроенные стили для оформления -->
  <style>
    /* Основные стили */
    body {
      font-family: 'Open Sans', sans-serif;
      line-height: 1.6;
      background: #f9f9f9;
      color: #333;
      margin: 0;
      padding: 0;
    }
    .container {
      width: 90%;
      max-width: 1200px;
      margin: 0 auto;
    }
    header, footer {
      background: #007acc;
      color: #fff;
      padding: 20px 0;
      text-align: center;
    }
    header h1, footer p {
      margin: 0;
    }
    /* Верстка навигации и контента */
    .sidebar {
      background: #fff;
      border-right: 1px solid #ddd;
      padding: 20px;
      width: 250px;
      position: fixed;
      top: 80px;
      bottom: 0;
      overflow-y: auto;
    }
    .sidebar h2 {
      font-size: 1.2em;
      margin-top: 0;
      color: #007acc;
    }
    .sidebar a {
      text-decoration: none;
      color: #007acc;
    }
    .sidebar a:hover {
      text-decoration: underline;
    }
    .content {
      margin-left: 270px;
      padding: 20px;
      background: #fff;
      min-height: calc(100vh - 160px);
    }
    article h1, article h2, article h3, article h4, article h5, article h6 {
      color: #007acc;
      margin-top: 1.5em;
    }
    article p {
      margin-bottom: 1em;
    }
    /* Таблицы */
    table {
      width: 100%;
      border-collapse: collapse;
      margin-bottom: 1em;
    }
    table, th, td {
      border: 1px solid #ddd;
    }
    th, td {
      padding: 8px;
      text-align: left;
    }
    th {
      background: #f0f0f0;
    }
    /* Пример стилей для кода */
    pre {
      background: #272822;
      color: #f8f8f2;
      padding: 15px;
      overflow-x: auto;
      border-radius: 4px;
    }
    code {
      font-family: Consolas, Menlo, Monaco, "Courier New", monospace;
    }
    /* Верстка переключателя версий */
    .version-switcher {
      margin-top: 10px;
    }
    .version-switcher select {
      padding: 5px;
      border: none;
      border-radius: 3px;
      font-size: 1em;
    }
    /* Стили для TOC внутри контента */
    .table-of-contents {
      background: #f7f7f7;
      padding: 10px 20px;
      border: 1px solid #ddd;
      margin-bottom: 20px;
      border-radius: 4px;
    }
    .table-of-contents p {
      font-weight: bold;
      margin-top: 0;
    }
    .table-of-contents ol {
      padding-left: 20px;
    }
    .table-of-contents li {
      margin-bottom: 5px;
    }
    /* Футер */
    footer p {
      font-size: 0.9em;
    }
  </style>
</head>
<body>
  <header>
    <div class="container">
      <h1>GasFree Developer Documentation</h1>
      <div class="version-switcher">
        <label for="version-select">Версия:</label>
        <select id="version-select" onchange="location = this.value;">
          <option value="index.html" selected>1.0.0</option>
          <!-- Пример для более ранней версии -->
          <option value="ver/v0.9/index.html">0.9.0</option>
        </select>
      </div>
    </div>
  </header>

  <nav class="sidebar">
    <div class="container">
      <h2>Содержание</h2>
      <div class="table-of-contents">
        <p>Table of Contents</p>
        <ol>
          <li><a href="#overview"><strong>Overview</strong></a></li>
          <li><a href="#authorization-process"><strong>Authorization Process</strong></a></li>
          <li>
            <a href="#signature-algorithm-and-provider-endpoint"><strong>Signature Algorithm and Provider Endpoint</strong></a>
            <ol>
              <li><a href="#31-parameters">3.1 Parameters</a></li>
              <li><a href="#32-authorization-construction-and-signature">3.2 Authorization Construction and Signature</a></li>
              <li><a href="#33-provider-endpoint">3.3 Provider Endpoint</a></li>
            </ol>
          </li>
          <li><a href="#notes"><strong>Notes</strong></a></li>
          <li>
            <a href="#apis"><strong>APIs</strong></a>
            <ol>
              <li><a href="#api-authentication">API Authentication</a></li>
              <li><a href="#api-format-definition">API Format Definition</a></li>
              <li><a href="#get-apiv1configtokenall">GET /api/v1/config/token/all</a></li>
              <li><a href="#get-apiv1configproviderall">GET /api/v1/config/provider/all</a></li>
              <li><a href="#get-apiv1addressaccountaddress">GET /api/v1/address/{accountAddress}</a></li>
              <li><a href="#post-apiv1gasfreesubmit">POST /api/v1/gasfree/submit</a></li>
              <li><a href="#get-apiv1gasfreetraceid">GET /api/v1/gasfree/{traceId}</a></li>
            </ol>
          </li>
        </ol>
      </div>
    </div>
  </nav>

  <main class="content">
    <div class="container">
      <article id="doc-content">
        <!-- Начало документации -->
        <h1 id="gasfree-developer-documentation">GasFree Developer Documentation</h1>
        <p style="text-align: center; margin-bottom: 100px;">Ver: 1.0.0</p>
        
        <div class="table-of-contents">
          <p>Table of Contents</p>
          <ol>
            <li><a href="#overview"><strong>Overview</strong></a></li>
            <li><a href="#authorization-process"><strong>Authorization Process</strong></a></li>
            <li>
              <a href="#signature-algorithm-and-provider-endpoint"><strong>Signature Algorithm and Provider Endpoint</strong></a>
              <ol>
                <li><a href="#31-parameters">3.1 Parameters</a></li>
                <li><a href="#32-authorization-construction-and-signature">3.2 Authorization Construction and Signature</a></li>
                <li><a href="#33-provider-endpoint">3.3 Provider Endpoint</a></li>
              </ol>
            </li>
            <li><a href="#notes"><strong>Notes</strong></a></li>
            <li>
              <a href="#apis"><strong>APIs</strong></a>
              <ol>
                <li><a href="#api-authentication">API Authentication</a></li>
                <li><a href="#api-format-definition">API Format Definition</a></li>
                <li><a href="#get-apiv1configtokenall">GET /api/v1/config/token/all</a></li>
                <li><a href="#get-apiv1configproviderall">GET /api/v1/config/provider/all</a></li>
                <li><a href="#get-apiv1addressaccountaddress">GET /api/v1/address/{accountAddress}</a></li>
                <li><a href="#post-apiv1gasfreesubmit">POST /api/v1/gasfree/submit</a></li>
                <li><a href="#get-apiv1gasfreetraceid">GET /api/v1/gasfree/{traceId}</a></li>
              </ol>
            </li>
          </ol>
        </div>

        <!-- 1. Overview -->
        <h2 id="overview">1. Overview</h2>
        <p>
          GasFree aims to provide users with a TRC-20/ERC-20 transfer solution that does not require a native token to pay for transaction gas fees. It specifically includes four roles: GasFree accounts, Service-Providers, wallets, and users, as shown in Figure 1 below.
        </p>
        <p style="text-align: center;"><em>Figure 1. GasFree Framework</em></p>
        <p>
          <strong>GasFree Account:</strong> Generated according to a specific algorithm. Its permissions are controlled by the user's EOA (Externally Owned Account) address. The user can sign a signature to authorize GasFree transfer of this account.
        </p>
        <p>
          <strong>Service-Provider:</strong> The GasFree service-provider is responsible for collecting users' GasFree transfer authorizations, submitting them to the blockchain, and paying the gas fees on behalf of the users. The Service-Provider may charge a certain handling fee after the transaction is completed.
        </p>
        <p>
          <strong>Wallet:</strong> After connecting to the GasFree service, the wallet provides end-users with interface functions such as fund inquiry for GasFree accounts and signature for transfer authorization.
        </p>

        <!-- 2. Authorization Process -->
        <h2 id="authorization-process">2. Authorization Process</h2>
        <p>
          Integrating GasFree into the wallet involves processes such as constructing transfer authorization, signing the transfer authorization, and the provider submitting the authorization to the blockchain on behalf of the user. For detailed information about the Provider API interface, please refer to Section 5 of this document. After the integration, the main interaction process is as follows:
        </p>
        <ol>
          <li>
            <p><strong>Prerequisite:</strong></p>
            <ul>
              <li>Call <code>/api/v1/config/token/all</code> to obtain the list of supported tokens.</li>
              <li>If a token that is not supported by the Provider is transferred into a GasFree account, the user should use the withdrawal page at <a href="https://gasfree.io/withdraw" target="_blank">https://gasfree.io/withdraw</a> to withdraw the token to their EOA address.</li>
              <li>Call <code>/api/v1/config/provider/all</code> to obtain the list of available Service-Providers.</li>
              <li>The GasFree account is inactive by default and will be activated during the first GasFree transfer. An additional <code>activation fee</code> will be charged during activation; subsequent transfers only incur the <code>transfer fee</code>.</li>
            </ul>
          </li>
          <li>
            <p><strong>Preparation:</strong></p>
            <ul>
              <li>Call <code>/api/v1/address/{accountAddress}</code> to query the GasFree account info (status, balance, nonce) and construct the transfer authorization accordingly.</li>
            </ul>
          </li>
          <li>
            <p><strong>Sign authorization:</strong></p>
            <ul>
              <li>The signature algorithm is based on EIP712. Refer to Section 3.2 for details.</li>
            </ul>
          </li>
          <li>
            <p><strong>Submit authorization:</strong></p>
            <ul>
              <li>Use <code>/api/v1/gasfree/submit</code> to send the signed transfer authorization to the Service-Provider.</li>
            </ul>
          </li>
          <li>
            <p><strong>Handling of provider response:</strong></p>
            <ul>
              <li>If successful, the provider returns a unique <code>traceId</code> which can be used to track the on-chain status.</li>
              <li>If failed, the wallet must notify the user that the authorization was rejected and no on-chain transaction will occur.</li>
            </ul>
          </li>
          <li>
            <p>
              <strong>Monitoring of the transfer authorization:</strong> Call <code>/api/v1/gasfree/{traceId}</code> to query the status of the authorization.
            </p>
          </li>
        </ol>

        <!-- 3. Signature Algorithm and Provider Endpoint -->
        <h2 id="signature-algorithm-and-provider-endpoint">3. Signature Algorithm and Provider Endpoint</h2>
        <h3 id="31-parameters">3.1 Parameters</h3>
        <p>
          The GasFree transfer authorization involves the following parameters. Their values on the TRON mainnet and the Nile testnet are shown in Table 1.
        </p>
        <table>
          <thead>
            <tr>
              <th>Parameter</th>
              <th>TRON - mainnet</th>
              <th>TRON - Nile testnet</th>
            </tr>
          </thead>
          <tbody>
            <tr>
              <td>chainId</td>
              <td>728126428</td>
              <td>3448148188</td>
            </tr>
            <tr>
              <td>verifyingContract</td>
              <td>TFFAMQLZybALaLb4uxHA9RBE7pxhUAjF3U</td>
              <td>THQGuFzL87ZqhxkgqYEryRAd7gqFqL5rdc</td>
            </tr>
          </tbody>
        </table>
        <p style="text-align: center;"><em>Table 1. GasFree Transfer Authorization Parameters</em></p>

        <h3 id="32-authorization-construction-and-signature">3.2 Authorization Construction and Signature</h3>
        <p><strong>General structure</strong></p>
        <p><em>MessageDomain:</em></p>

<pre><code>const Permit712MessageDomain = {
  name: 'GasFreeController',
  version: 'V1.0.0',
  chainId: 3448148188, // tronWeb.toDecimal('0xcd8690dc'),
  verifyingContract: 'THQGuFzL87ZqhxkgqYEryRAd7gqFqL5rdc'
};
</code></pre>

        <p><em>Field description:</em></p>
        <ul>
          <li>token: address of transferring token</li>
          <li>name: 'GasFreeController' (fixed)</li>
          <li>version: 'V1.0.0' (fixed)</li>
          <li>chainId: as specified in Section 3.1</li>
          <li>verifyingContract: as specified in Section 3.1</li>
        </ul>
        <p><em>MessageTypes: fixed value</em></p>

<pre><code>const Permit712MessageTypes = {
  PermitTransfer: [
    { name: 'token', type: 'address' },
    { name: 'serviceProvider', type: 'address' },
    { name: 'user', type: 'address' },
    { name: 'receiver', type: 'address' },
    { name: 'value', type: 'uint256' },
    { name: 'maxFee', type: 'uint256' },
    { name: 'deadline', type: 'uint256' },
    { name: 'version', type: 'uint256' },
    { name: 'nonce', type: 'uint256' }
  ]
};
</code></pre>

        <p><em>Message body:</em></p>

<pre><code>const message = {
  token: 'TXYZopYRdj2D9XRtbG411XZZ3kM5VkAeBf',
  serviceProvider: 'TKtWbdzEq5ss9vTS9kwRhBp5mXmBfBns3E',
  user: 'THvMiWQeVPGEMuBtAnuKn2QpuSjqjrGQGu',
  receiver: 'TMDKznuDWaZwfZHcM61FVFstyYNmK6Njk1',
  value: '90000000',
  maxFee: '20000000',
  deadline: '1728638679',
  version: 1,
  nonce: 0
};
</code></pre>

        <p><strong>Sign with Wallet</strong></p>
        <p>Using the above structure, the TRON wallet (for example, via TronLink) will sign the EIP712 message and return the <code>sig</code> parameter. Example:</p>

<pre><code>const signature = await window.tron.tronWeb.trx._signTypedData(
  Permit712MessageDomain,
  Permit712MessageTypes,
  message
); // remove 0x if present
</code></pre>

        <h3 id="33-provider-endpoint">3.3 Provider Endpoint</h3>
        <p>
          Wallets/users interact with the Provider through the APIs under the Provider endpoint, including submitting GasFree transfer authorizations and querying their statuses.
        </p>
        <ul>
          <li>TRON mainnet: <a href="https://openapi.gasfree.io" target="_blank">https://openapi.gasfree.io</a></li>
          <li>TRON Nile testnet: <a href="https://test-nile.gasfree.io" target="_blank">https://test-nile.gasfree.io</a></li>
        </ul>
        <p><em>Note: Currently, GasFree only provides services in the TRON network and can be extended to Ethereum and other EVM chains in the future.</em></p>

        <!-- 4. Notes -->
        <h2 id="notes">4. Notes</h2>
        <ol>
          <li style="color: red;"><strong>It is not recommended that the testnet environment be provided to users.</strong></li>
        </ol>
        <p><strong>The GasFree environment on the TRON testnet is for developer testing only.</strong></p>
        <p><strong>It is strongly recommended to disable the testnet for ordinary users after official launch to avoid asset loss.</strong></p>
        <ol start="2">
          <li><strong>It is recommended to verify balance and status before submitting a transfer authorization. See the GasFree account interface definition.</strong></li>
        </ol>
        <p><strong>Unless otherwise specified, all asset amounts are in the smallest unit.</strong></p>

        <!-- 5. APIs -->
        <h2 id="apis">5. APIs</h2>

        <h3 id="api-authentication">API Authentication</h3>
        <p>
          After applying for access, you will receive an API Key and API Secret. These are used to sign API requests.
          Keep your API Secret confidential. The signature is transmitted via the HTTP header.
        </p>
        <p>Please contact GasFree for your API Key and API Secret.</p>
        <p><strong>HTTP header definition:</strong></p>

<pre><code>{
  "Timestamp": 1731912286, // unit: second
  "Authorization": "ApiKey {api_key}:{signature}"
}
</code></pre>

        <p><strong>API Signature and Authentication</strong></p>
        <ol>
          <li>Construct a string from the request method, path, and timestamp.</li>
          <li>Calculate the signature using HMAC-SHA256 with your API secret, then base64 encode the result.</li>
          <li>Add the signature to the request header.</li>
        </ol>
        <p><strong>Example (Python):</strong></p>

<pre><code>import hmac
import hashlib
import base64
import time
import requests

API_KEY = 'YOUR_API_KEY'
API_SECRET = 'YOUR_API_SECRET'

method = 'GET'
path = '/api/v1/config/token/all'
timestamp = int(time.time())
message = f'{method}{path}{timestamp}'
signature = base64.b64encode(
    hmac.new(
        API_SECRET.encode('utf-8'),
        message.encode('utf-8'),
        hashlib.sha256
    ).digest()
).decode('utf-8')

url = 'https://test-nile.gasfree.io' + path
headers = {
  'Timestamp': f'{timestamp}',
  'Authorization': f'ApiKey {API_KEY}:{signature}'
}

response = requests.get(url, headers=headers)
print(response.json())
</code></pre>

        <p><strong>API Format Definition</strong></p>
        <p>
          When the service runs normally, the HTTP code is <code>200</code>. Errors (input or runtime) are indicated in the HTTP body.
        </p>

<pre><code>{
  "code": 200, // 200: OK, 400: input error, 500: runtime error
  "reason": null, // Exception name (if any)
  "message": "",  // Error details
  "data": ""      // API return data, or null if none
}
</code></pre>

        <p><strong>Error return example:</strong></p>

<pre><code>{
  "code": 400,
  "reason": "GasFreeAddressNotFoundException",
  "message": "123",
  "data": null
}
</code></pre>

        <p><strong>Successful return example:</strong></p>

<pre><code>{
  "code": 200,
  "reason": null,
  "message": null,
  "data": {
    "tokens": [
      {
        "tokenAddress": "TXYZopYRdj2D9XRtbG411XZZ3kM5VkAeBf",
        "createdAt": "2024-09-10T09:46:24.801+00:00",
        "updatedAt": "2024-09-11T06:57:10.244+00:00",
        "activateFee": 10000000,
        "transferFee": 10000000,
        "supported": true,
        "symbol": "USDT",
        "decimal": 6
      }
    ]
  }
}
</code></pre>

        <h3 id="get-apiv1configtokenall">GET /api/v1/config/token/all</h3>
        <p>Get the contract list of all supported tokens.</p>
        <ul>
          <li><strong>Request parameters:</strong> None</li>
          <li><strong>Return:</strong> <code>tokens</code> – list of token objects.</li>
        </ul>
        <p><em>Token object field description:</em></p>
        <ul>
          <li>tokenAddress: token contract address</li>
          <li>activateFee: activation fee in smallest unit</li>
          <li>transferFee: transfer fee in smallest unit</li>
          <li>symbol: token name</li>
          <li>decimal: token precision</li>
        </ul>

<pre><code>{
  "code": 200,
  "reason": null,
  "message": null,
  "data": {
    "tokens": [
      {
        "tokenAddress": "TXYZopYRdj2D9XRtbG411XZZ3kM5VkAeBf",
        "createdAt": "2024-10-09T08:14:12.560+00:00",
        "updatedAt": "2024-10-09T08:14:12.560+00:00",
        "activateFee": 10000000, // 10 USDT
        "transferFee": 10000000, // 10 USDT
        "supported": true,
        "symbol": "USDT",
        "decimal": 6
      }
    ]
  }
}
</code></pre>

        <h3 id="get-apiv1configproviderall">GET /api/v1/config/provider/all</h3>
        <p>Get the list of all supported service providers.</p>
        <ul>
          <li><strong>Request parameters:</strong> None</li>
          <li><strong>Return:</strong> <code>providers</code> – list of provider objects.</li>
        </ul>
        <p><em>Provider object field description:</em></p>
        <ul>
          <li>address: Service-Provider address</li>
          <li>name: Provider’s name</li>
          <li>icon: Provider’s icon</li>
          <li>website: Provider’s website</li>
          <li>config: Object with parameters:
            <ul>
              <li>maxPendingTransfer</li>
              <li>minDeadlineDuration</li>
              <li>maxDeadlineDuration</li>
              <li>defaultDeadlineDuration</li>
            </ul>
          </li>
        </ul>

<pre><code>{
  "code": 200,
  "reason": null,
  "message": null,
  "data": {
    "providers": [
      {
        "address": "TQ6qStrS2ZJ96gieZJC8AurTxwqJETmjfp",
        "name": "Provider-1",
        "icon": "",
        "website": "",
        "config": {
          "maxPendingTransfer": 1,
          "minDeadlineDuration": 60,
          "maxDeadlineDuration": 600,
          "defaultDeadlineDuration": 180
        }
      }
    ]
  }
}
</code></pre>

        <h3 id="get-apiv1addressaccountaddress">GET /api/v1/address/{accountAddress}</h3>
        <p>Query the user's GasFree account info (activation status, nonce, supported tokens, assets).</p>
        <ul>
          <li><strong>Request parameters:</strong> <code>accountAddress</code> (user's EOA address)</li>
          <li><strong>Return:</strong> Asset info object.</li>
        </ul>
        <p><em>Asset info field description:</em></p>
        <ul>
          <li>accountAddress, gasFreeAddress, active, nonce, allow_submit</li>
          <li>assets: Array of asset objects (tokenAddress, tokenSymbol, activateFee, transferFee, decimal, frozen)</li>
        </ul>

<pre><code>{
  "code": 200,
  "reason": null,
  "message": null,
  "data": {
    "accountAddress": "TKtWbdzEq5ss9vTS9kwRhBp5mXmBfBns3E",
    "gasFreeAddress": "TLGVf7MRsLG7XxBkJKy8wnCVcDnAeXYNCb",
    "active": true,
    "nonce": 1,
    "allow_submit": false,
    "assets": [
      {
        "tokenAddress": "TXYZopYRdj2D9XRtbG411XZZ3kM5VkAeBf",
        "tokenSymbol": "USDT",
        "activateFee": 10000000,
        "transferFee": 10000000,
        "decimal": 6,
        "frozen": 0
      }
    ]
  }
}
</code></pre>

        <h3 id="post-apiv1gasfreesubmit">POST /api/v1/gasfree/submit</h3>
        <p>Initiate a GasFree transfer authorization.</p>
        <ul>
          <li><strong>Request parameters:</strong>
            <ul>
              <li>token: token address</li>
              <li>provider: Service-Provider address</li>
              <li>user: user's EOA address (not GasFree address)</li>
              <li>receiver: recipient address</li>
              <li>value: transfer amount</li>
              <li>maxFee: maximum fee limit (transfer fee + activation fee)</li>
              <li>deadline: expiration timestamp (in seconds)</li>
              <li>version: signature version (currently 1)</li>
              <li>nonce: nonce value</li>
              <li>sig: user's signature</li>
            </ul>
          </li>
        </ul>
        <p><strong>Return:</strong> Basic information of the transfer authorization.</p>

<pre><code>{
  "token": "TXYZopYRdj2D9XRtbG411XZZ3kM5VkAeBf",
  "provider": "TCETRh3aED4kdkaYQY7CcxeTJtrQvwBpNT",
  "user": "TKtWbdzEq5ss9vTS9kwRhBp5mXmBfBns3E",
  "receiver": "TEkj3ndMVEmFLYaFrATMwMjBRZ1EAZkucT",
  "value": 100000,
  "maxFee": 1000000,
  "deadline": 1728638679,
  "version": 1,
  "nonce": 9,
  "sig": "9dfd3638e03af56bc93fa619e20e1e743f6b5c0d9a49bd340a94e27f6d6a6413618cc8481b9d5816a793982d8047daa0badbade02f92814e78a9894efd9877341b"
}
</code></pre>

        <p><em>Field description:</em></p>
        <ul>
          <li>id: traceId (not transactionId)</li>
          <li>accountAddress, gasFreeAddress, providerAddress, targetAddress, tokenAddress</li>
          <li>amount, maxFee, signature, version, nonce, expiredAt, state</li>
          <li>estimatedActivateFee, estimatedTransferFee</li>
        </ul>
        <p><strong>Successful return example:</strong></p>

<pre><code>{
  "code": 200,
  "reasone": null,
  "message": null,
  "data": {
    "id": "6ab4c27c-f66b-4328-b40f-ffdc6cf1ca60",
    "createdAt": "2024-09-10T08:11:50.822+00:00",
    "updatedAt": "2024-09-10T08:11:50.822+00:00",
    "accountAddress": "TKtWbdzEq5ss9vTS9kwRhBp5mXmBfBns3E",
    "gasFreeAddress": "TLGVf7MRsLG7XxBkJKy8wnCVcDnAeXYNCb",
    "providerAddress": "TQ6qStrS2ZJ96gieZJC8AurTxwqJETmjfp",
    "targetAddress": "TQ6qStrS2ZJ96gieZJC8AurTxwqJETmjfp",
    "tokenAddress": "TXYZopYRdj2D9XRtbG411XZZ3kM5VkAeBf",
    "amount": 1000000,
    "maxFee": 1000000,
    "signature": "f5bb43b90a5295759819edb029a1c2d6cd50acc9bd4283fd73c4be16fe163d154ec4f06fd70c8d63cc2ff2346ea1c86abf019da944fb62eb28fe0a8f6e12e1931c",
    "nonce": 0,
    "expiredAt": "2024-09-11T08:05:08.000+00:00",
    "state": "WAITING",
    "estimatedActivateFee": 1000,
    "estimateTransferFee": 300
  }
}
</code></pre>

        <p><strong>Error example:</strong></p>

<pre><code>{
  "code": 400,
  "reason": "DeadlineExceededException",
  "message": "deadline exceeded",
  "data": null
}
</code></pre>

        <p><em>Error types include:</em></p>
        <ul>
          <li>ProviderAddressNotMatchException</li>
          <li>DeadlineExceededException</li>
          <li>InvalidSignatureException</li>
          <li>UnsupportedTokenException</li>
          <li>TooManyPendingTransferException</li>
          <li>VersionNotSupportedException</li>
          <li>NonceNotMatchException</li>
          <li>MaxFeeExceededException</li>
          <li>InsufficientBalanceException</li>
        </ul>

        <h3 id="get-apiv1gasfreetraceid">GET /api/v1/gasfree/{traceId}</h3>
        <p>Query the details of a specified GasFree transfer authorization. (Note: If queried too early or if verification fails, transaction-related fields will be empty.)</p>
        <ul>
          <li><strong>Required parameter:</strong> <code>traceId</code></li>
          <li><strong>Return:</strong> Detailed info of the transfer authorization.</li>
        </ul>
        <p><em>Field description:</em></p>
        <ul>
          <li>id, createdAt, accountAddress, gasFreeAddress, providerAddress, targetAddress, nonce, tokenAddress</li>
          <li>amount, expiredAt, state</li>
          <li>estimatedActivateFee, estimatedTransferFee, estimatedTotalFee, estimatedTotalCost</li>
          <li>txnHash, txnBlockNum, txnBlockTimestamp, txnState, txnActivateFee, txnTransferFee, txnTotalFee, txnAmount, txnTotalCost</li>
        </ul>
      </article>
    </div>

  </main>

  <footer>
    <div class="container">
      <p>&copy; 2025 GasFree. Все права защищены.</p>
    </div>
  </footer>

  <!-- При необходимости можно добавить JavaScript для интерактивности -->
  <script>
    // Пример: можно реализовать динамическое сворачивание разделов или другие эффекты
  </script>
</body>
</html>
