## Ethereum.Database

A Blockchain is essentially a decentralized database that runs on a peer-to-peer network. You can use [Blockchain Web Services](https://bweb.services) `Ethereum.Database.Immutable` and `Ethereum.Database.Mutable` contracts to save and get data from such database.

| Operation     | Description                                   |
| ------------- | --------------------------------------------- |
| insertBytes32 | Saves up to 32 Bytes of data to Blockchain    |
| selectBytes32 | Gets from Blockchain previously inserted data |
| insertString  | Saves a string to Blockchain                  |
| selectString  | Gets from Blockchain previously inserted data |

The use of `insertBytes32` is cheaper than `insertString` (check [Required Funds](#required-funds)).

<aside class="warning">
Same operations are available for Immutable and Mutable behaviour.
</aside>

<a name="ethereum-database-immutable"></a>

### Ethereum.Database.Immutable

"_An immutable object is an object whose state cannot be modified after it is created_"

#### Contract Address

Click on Contract Address to check verified contract at `etherscan.io`.

| Network Id | Contract Address                                                                                                                   | Version |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------- | ------- |
| ethereum   |
| ropsten    | [0x81D575b53239BcB4332bb1608a21F1A17035deeA](https://ropsten.etherscan.io/address/0x81D575b53239BcB4332bb1608a21F1A17035deeA#code) | 2       |

##### insertBytes32

> insertBytes32 operation call example.

```javascript
var parameters = {
  contract: "Ethereum.Database.Immutable",
  version: 2,
  network: "ropsten",
  operation: "insertBytes32",
  parameters: {
    key: "a-key",
    value: "Hello World!",
  },
};

$.ajax({
  method: "POST",
  url: "https://api.bweb.services/v1/call",
  data: JSON.stringify(parameters),
  headers: {
    "Content-Type": "application/json",
    "X-Api-Key": "ExV0d92KzQ8QgsTVnevddpbB8cUaAfPs7ntVF8g0",
  },
  dataType: "json",
  success: function (response) {
    console.log(response);
  },
  error: function (xhr, textStatus, errorThrown) {
    console.log(xhr);
  },
});
```

> If successfull, the call will return the related Job Id to fetch for results.

```json
{
  "statusCode": 200,
  "info": {
    "jobId": "543433243"
  }
}
```

Saves up to 32 characters string value in Ethereum database (check [Passing Parameters](#passing-parameters) for other required parameters).

| Parameter  | Value                                                                     |
| ---------- | ------------------------------------------------------------------------- |
| contract   | Ethereum.Database.Immutable                                               |
| operation  | insertBytes32                                                             |
| parameters | [insertBytes32 Operation Parameters](#insertBytes32-operation-parameters) |

<a name="insertBytes32-operation-parameters"></a>

###### insertBytes32 Operation Parameters

The following operation parameters can be used to save a string you can later query by using the `key`value.

| Parameter | Type   | Value(s)             | Description                    |
| --------- | ------ | -------------------- | ------------------------------ |
| key       | string | 32 characters string | The key for data to save.      |
| value     | string | 32 characters string | The value to save on database. |

###### insertBytes32 Response

The operation call will return the `jobId` of the job running on Blochchain Web Services to execute your command (remember blockchain operations are asynchronous and can take a while to finish).

`{ "statusCode": 200, "info": { "jobId": "543433243" } }`

##### selectBytes32

> selectBytes32 operation parameters call example.

```javascript
var parameters = {
  contract: "Ethereum.Database.Immutable",
  version: 2,
  network: "ropsten",
  operation: "selectBytes32",
  parameters: {
    key: "a-key",
  },
};

...

```

Gets a value you previously stored on Ethereum using `insertBytes32` (check [Passing Parameters](#passing-parameters) for other required parameters).

| Parameter  | Value                                                                     |
| ---------- | ------------------------------------------------------------------------- |
| contract   | Ethereum.Database.Immutable                                               |
| operation  | selectBytes32                                                             |
| parameters | [selectBytes32 Operation Parameters](#selectBytes32-operation-parameters) |

###### selectBytes32 Operation Parameters

Set the `key` value to get the data you previously saved.

| Parameter | Type   | Value(s)             | Description               |
| --------- | ------ | -------------------- | ------------------------- |
| key       | string | 32 characters string | The key for data to save. |

###### selectBytes32 Response

The operation call will return the `jobId` of the job running on Blochchain Web Services to execute your command (remember blockchain operations are asynchronous and can take a while to finish).

`{ "statusCode": 200, "info": { "jobId": "543433243" } }`

<a name="insertString-operation"></a>

##### insertString

> insertString operation parameters call example.

```javascript
var parameters = {
  contract: "Ethereum.Database.Immutable",
  version: 2,
  network: "ropsten",
  operation: "insertString",
  parameters: {
    key: "a-key",
    value: "Hello World!",
  },
};

...

```

Saves a string value in Ethereum database.

| Parameter  | Value                                                                   |
| ---------- | ----------------------------------------------------------------------- |
| contract   | Ethereum.Database.Immutable                                             |
| operation  | insertBytes32                                                           |
| parameters | [insertString Operation Parameters](#insertString-operation-parameters) |

Check [Passing Parameters](#passing-parameters) for other required parameters.

###### insertString Operation Parameters

The following operation parameters can be used to save a string you can later query by using the `key`value.

| Parameter | Type   | Description                    |
| --------- | ------ | ------------------------------ |
| key       | string | The key for data to save.      |
| value     | string | The value to save on database. |

###### insertString Response

The operation call will return the `jobId` of the job running on Blochchain Web Services to execute your command (remember blockchain operations are asynchronous and can take a while to finish).

`{ "statusCode": 200, "info": { "jobId": "5434323243" } }`

<a name="selectString-operation"></a>

##### selectString

> selectString operation parameters call example.

```javascript
var parameters = {
  contract: "Ethereum.Database.Immutable",
  version: 2,
  network: "ropsten",
  operation: "selectString",
  parameters: {
    key: "a-key",
  },
};

...

```

Gets a value you previously stored on Ethereum using `insertString`.

| Parameter  | Value                                                                   |
| ---------- | ----------------------------------------------------------------------- |
| contract   | Ethereum.Database.Immutable                                             |
| operation  | selectString                                                            |
| parameters | [selectString Operation Parameters](#selectString-operation-parameters) |

Check [Passing Parameters](#passing-parameters) for other required parameters.

###### selectString Operation Parameters

Set the `key` value to get the data you previously saved.

| Parameter | Type   | Description               |
| --------- | ------ | ------------------------- |
| key       | string | The key for data to save. |

###### selectString Response

The operation call will return the `jobId` of the job running on Blochchain Web Services to execute your command (remember blockchain operations are asynchronous and can take a while to finish).

`{ "statusCode": 200, "info": { "jobId": "5423433243" } }`

### Ethereum.Database.Mutable

> Mutable insertString operation parameters call example.

```javascript
var parameters = {
  contract: "Ethereum.Database.Mutable",
  version: 1,
  network: "ropsten",
  operation: "insertString",
  parameters: {
    key: "a-key",
    value: "Hello World!",
  },
};
```

Mutable insert operations can overwrite previously saved data and the same insert/select operations are available for `Ethereum.Database.Mutable` contract (you just need to replace `contract` and `version` parameter to use Mutable or Immutable contract).

#### Contract Address

| Network Id | Contract Address                                                                                                                   | Version |
| ---------- | ---------------------------------------------------------------------------------------------------------------------------------- | ------- |
| ethereum   |
| ropsten    | [0x9089Db83F0590EC2eD01A5Eb4F8584Dd6F4bDaC7](https://ropsten.etherscan.io/address/0x9089Db83F0590EC2eD01A5Eb4F8584Dd6F4bDaC7#code) | 1       |
