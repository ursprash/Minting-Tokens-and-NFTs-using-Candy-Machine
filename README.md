# Minting-Tokens-and-NFTs-using-Candy-Machine
Creating a full UI for a Candy Machine and setting up an SPL token involves multiple steps, and it's beyond the scope of a single response. However, I can provide you with an outline of the process and the necessary steps to get started.

## Project Overview

![Solana Logo](https://cryptologos.cc/logos/solana-sol-logo.png?v=024)

1.Create an SPL token.
2.You will need to tweak your config.json to use the splTokenAddress of the token you created in Step 1.
3.Create a UI for your candy machine 

## Getting Started

1. Set Up Your Environment:
   - Make sure you have Node.js and npm (Node Package Manager) installed on your computer.

2. Create a React Application:
   - Initialize a new React application using Create React App or your preferred React setup.

3. Set Up a New Wallet
   - We first need to create a new wallet for specifically devnet testing

```bash
solana-keygen new --outfile ./wallet.json
```

We can skip the password (by hitting Enter) as we will only use this wallet on devnet, so the funds are not important. We can confirm that the wallet we just generated is the wallet that the Solana CLI will use by running: 

```bash
solana config set --keypair ./wallet.json
```

4.Establish a Connection to Your QuickNode RPC
We will need to make sure our Solana CLI is connected to a node. You're welcome to use public nodes or deploy and manage your own infrastructure, however, if you'd like 8x faster response times you can leave the heavy lifting to us.
With your endpoint on the Solana Devnet setup, you can now run this command, substituting YOUR_QUICKNODE_URL with the HTTP URL you have copied:

```bash
solana config set --url YOUR_QUICKNODE_URL
```

Now to fund your wallet you can run the command:

```bash
solana airdrop 5
```

## Prepare NFT Assets
1.Configure Candy Machine
Create a new file, config.json in your root project folder: 

```bash
echo > config.json
```

Open the file and paste this config: 

```bash
{
    "price": 0.01,
    "number": 10,
    "symbol": "NB",
    "sellerFeeBasisPoints": 500,
    "gatekeeper": null,
    "solTreasuryAccount": "YOUR_WALLET_ADDRESS",
    "splTokenAccount": null,
    "splToken": null,
    "goLiveDate": "2022-07-24T00:00:00Z",
    "endSettings": null,
    "whitelistMintSettings": null,
    "hiddenSettings": null,
    "uploadMethod": "bundlr",
    "awsS3Bucket": null,
    "retainAuthority": true,
    "isMutable": true,
    "creators": [
    {
      "address": "YOUR_WALLET_ADDRESS",
      "share": 100
    }
  ]
}
```

2.Sugar has a built in validation error that will let us check for any errors before we proceed. In terminal, run: 
```bash
sugar validate
```

## Create Candy Machine

1.Upload Your Assets:
```bash
sugar upload
```
2.Deploy Candy Machine:

```bash
sugar deploy
```
3.Verify Candy Machine:

```bash
sugar verify
```
4.Test Your Candy Machine:
```bash
sugar mint
```
5.Set Up a Minting Site
For the easiest possible set up, we will be using the front end that Metaplex provides us, Candy Machine UI. 

From your project directory, in your terminal enter: 
```bash
git clone https://github.com/metaplex-foundation/candy-machine-ui ./candy-machine-ui/
cd candy-machine-ui
```
Rename the file .env.example to .env. After changing the file name, you can change the values in there to the following:

```bash
REACT_APP_CANDY_MACHINE_ID=<YOUR_CANDY_MACHINE_PUBKEY>
REACT_APP_SOLANA_NETWORK=devnet
REACT_APP_SOLANA_RPC_HOST=<YOUR_QUICKNODE_DEVNET_ENDPOINT>
```
If you don't remember your Candy Machine ID, you should be able to find it in cache.json in the program.candyMachine field. 

### NOTE:IN candy-machine ui update package.json file(in script section):  
```bash
"scripts": {
    "start": "export SET NODE_OPTIONS=--openssl-legacy-provider && craco start",
    "lint": "prettier -c 'src/**/*.{ts,tsx}' && npm run lint:eslint",
    "lint:eslint": "eslint 'src/**/*.{ts,tsx}'",
    "lint:fix": "prettier --write 'src/**/*.{ts,tsx}' && eslint --fix 'src/**/*.{ts,tsx}'",
    "build": "craco build",
    "test": "craco test",
    "eject": "craco eject"
  },
```

With all of that information plugged in, you can now save the file. From that candy-machine-ui folder, run the following commands:
```bash
npm install
npm start
```

## Installation

1. Clone this repository: `https://github.com/ursprash/Minting-Tokens-and-NFTs-using-Candy-Machine.git`

## Configuration

Edit the `config.json` file to configure your Candy Machine and SPL token settings.

## Usage

1. Start the development server: `npm start`
2. Open your browser and navigate to `http://localhost:3000` to use the UI.

## Output Of UI:
![Screenshot 2023-09-22 223313](https://github.com/ursprash/Minting-Tokens-and-NFTs-using-Candy-Machine/assets/111697531/d5720e4a-e059-4b11-ac82-eac84187b4e8)

![2](https://github.com/ursprash/Minting-Tokens-and-NFTs-using-Candy-Machine/assets/111697531/6a02335f-9131-4e15-8821-deacfd7c8876)

![4](https://github.com/ursprash/Minting-Tokens-and-NFTs-using-Candy-Machine/assets/111697531/ed46930d-2c0e-42ed-9dfb-182f76b8819b)

![3](https://github.com/ursprash/Minting-Tokens-and-NFTs-using-Candy-Machine/assets/111697531/afa5a7cb-1c99-43fe-9f01-7f9f9ecdb8e5)


## Contributor
ursprash

## License

This project is licensed under the [MIT License](LICENSE).
