## MegaLock.ninja

<pre style="background-color: initial; padding: 0 0 20px 0">
  <img src="images/megalock-snap-1.png" style="width:95%">
</pre>

[MegaLock.ninja](https://megalock.ninja/) is a website anyone can use to securely save data in Ethereum Blockchain.

<aside class="notice">
Data is encrypted and can only be accessed using linked email account.
</aside>

The website only needs 3 calls to **Blockchain Web Services** API to save data into Ropsten Network with no need to create any Blockchain account:

- [insertString](#insertString-operation) to save data to Ethereum blockchain,
- [selectString](#selectString-operation) to get encrypted data from the blockchain, and
- [fetch](#fetch-operation) to fetch API calls status.

Before data is sent to **Blockchain Web Services** [MegaLock.ninja](https://megalock.ninja/) creates RSA key pairs for each user to encrypt and secure data at REST on Ethereum distributed database.

`crypto.generateKeyPairSync("rsa", { modulusLength: 2048, });`

<aside class="warning">
User data, even encrypted will never be stored in BWS.
</aside>

### Saving Data in Ethereum

```js
async function callInsertStringBWSAPI(endpoint, key, value, apiKey) {
  var body = {
    contract: "Ethereum.Database.Mutable",
    version: 1,
    network: "ropsten",
    operation: "insertString",
    parameters: {
      key: key,
      value: value,
    },
  };

  const response = await fetch(endpoint + "/call", {
    method: "post",
    body: JSON.stringify(body),
    headers: {
      "Content-Type": "application/json",
      "X-Api-Key": apiKey,
    },
  });
  const result = await response.json();

  if (result.statusCode != 200) throw new Error(result.statusMessage);

  return result;
}
```

> Fetch API call status and receipt

```js
async function callFetchJobBWSAPI(endpoint, jobId, apiKey) {
  var body = {
    jobId: jobId,
  };

  const response = await fetch(endpoint + "/fetch", {
    method: "post",
    body: JSON.stringify(body),
    headers: { "Content-Type": "application/json", "X-Api-Key": apiKey },
  });
  const result = await response.json();

  if (result.statusCode != 200) throw new Error(result.statusMessage);

  return result;
}
```

Once the website validates your email address,

![Megalock.ninja](images/megalock-snap-2.png)

enter the data you want to secure in Ethereum database and just click SAVE button.

![Megalock.ninja](images/megalock-snap-3.png)

<aside class="warning">
Saving data in Ethereum is an asynchronous operation and can take a while.
</aside>

![Megalock.ninja](images/megalock-snap-4.png)

Once finished, you can check Blockchain transaction on Etherscan (an example for the transaction used for creating those snapshots: [https://ropsten.etherscan.io/tx/0x6a3d336dd1..](https://ropsten.etherscan.io/tx/0x6a3d336dd1792a786e0070cdd695fbc9526488258bfa5952579a60fde68323ce)).

![Megalock.ninja](images/megalock-snap-6.png)

Your data is now secured in Blockchain for ever ;)

### Getting Data from Ethereum

```js
async function callSelectStringBWSAPI(endpoint, key, apiKey) {
  var body = {
    contract: "Ethereum.Database.Mutable",
    version: 1,
    network: "ropsten",
    operation: "selectString",
    parameters: {
      key: key,
    },
  };

  const response = await fetch(endpoint + "/call", {
    method: "post",
    body: JSON.stringify(body),
    headers: {
      "Content-Type": "application/json",
      "X-Api-Key": apiKey,
    },
  });
  const result = await response.json();

  if (result.statusCode != 200) throw new Error(result.statusMessage);

  return result;
}
```

Getting you password from Ethereum blockchain is similar to saving. You validate the email you used to save and [MegaLock.ninja](https://megalock.ninja/) will call Blockchain Web services to fetch your data.

![Megalock.ninja](images/megalock-snap-8.png)

As for saving, fetching data can take a while, but for reading data from Blockchain it usually goes much faster.

![Megalock.ninja](images/megalock-snap-9.png)

You will get the password or any saved data, copy it to the clipboard and use it as required.

![Megalock.ninja](images/megalock-snap-10.png)
