**Welcome to Pump.fun API 👾**
-------------------------------------

Documentation for **3rd-Party Pump.fun API** to buy and sell programatically on [pump.fun](https://pump.fun/)

## Buy
```typescript
import { VersionedTransaction, Connection, Keypair } from '@solana/web3.js';
import bs58 from "bs58";

const RPC_ENDPOINT = "https://api.mainnet-beta.solana.com";
const web3Connection = new Connection(RPC_ENDPOINT,'confirmed');

const response = await fetch(`https://api.pumpdata.fun/buy`, {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({
        "mint": "pump.fun_token_address_",                // the token address from pump.fun
        "buyerPublicKey": "your_public_solana_wallet",    // Your wallet public key
        "amountInSol": 0.1,                               // amount of SOL, (0.1 SOL)
        "slippagePercent": 25,                            // percent slippage allowed (25%)
        "priorityFee": 0.0001,                            // priority fee (0.0001 SOl)
    })
});

if(response.status === 200) {
    const data = await response.arrayBuffer();
    const tx = VersionedTransaction.deserialize(new Uint8Array(data));
    const signerKeyPair = Keypair.fromSecretKey(bs58.decode("your_solana_wallet_private_key"));

    tx.sign([signerKeyPair]);
    const signature = await web3Connection.sendTransaction(tx)

    console.log("Transaction: https://solscan.io/tx/" + signature);
} else {
    console.log(response.statusText);
}

```

## Sell
```typescript
import { VersionedTransaction, Connection, Keypair } from '@solana/web3.js';
import bs58 from "bs58";

const RPC_ENDPOINT = "https://api.mainnet-beta.solana.com";
const web3Connection = new Connection(RPC_ENDPOINT,'confirmed');

const response = await fetch(`https://api.pumpdata.fun/sell`, {
    method: "POST",
    headers: {
        "Content-Type": "application/json"
    },
    body: JSON.stringify({
        "mint": "pump.fun_token_address_",                // the token address from pump.fun
        "sellerPublicKey": "your_public_solana_wallet",   // Your wallet public key
        "tokens": 35733.3,                                // amount of tokens, (35733.3 Doge tokens)
        "slippagePercent": 25,                            // percent slippage allowed (25%)
        "priorityFee": 0.0001,                            // priority fee (0.0001 SOl)
    })
});

if(response.status === 200) {
    const data = await response.arrayBuffer();
    const tx = VersionedTransaction.deserialize(new Uint8Array(data));
    const signerKeyPair = Keypair.fromSecretKey(bs58.decode("your_solana_wallet_private_key"));

    tx.sign([signerKeyPair]);
    const signature = await web3Connection.sendTransaction(tx)

    console.log("Transaction: https://solscan.io/tx/" + signature);
} else {
    console.log(response.statusText);
}

```
