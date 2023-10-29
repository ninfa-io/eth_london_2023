![](https://ninfa.io/static/media/darklogo.649655b0.png)
Wallet-less web2 authentication and UX for web3 DAPPs
=======================

**Live Demo**: [Link](https://hackathon-starter-1.ydftech.com/)

// TODO Firebase build

**Swimlanes Diagram**: [Link](https://swimlanes.io/u/de98ILCjT) exemplifying start-to-finish web2 user journery from onboarding with their web2 accounts to becoming a web3 citizen without having to change their original address, thanks to Account Abstraction!

An fully functional NFT marketplace for web2 (and web3) users.

Collectors can buy, sell and transfer NFTs without ever creating a crypto wallet or
paying for gas. Any NFT or ETH is sent to an Account Abstraction contract ('s predicted address), whose owner is an MPC wallet (or Multisig owned by one or more wallets) created and
controlled by any web2 authentication method, OAuth, OTP or WebAuthn.

## Table of Contents

[ToC]

## Features

- Web2 Onboarding and Transacting with Blockchain
  - **OTP Authentication:** using Email with magic link
  - **OAuth 2.0 Authentication:** Sign in with Google, Facebook, Twitter, LinkedIn, Twitch, Github, Snapchat
  - **Web3 Authentication:** Via web3 wallet provider such as Metamask
- **User Profile and NFT Management**
  - See collected NFTs
  - Sell and Transfer owned NFTs
  - Link multiple web2 authentication strategies to the same ERC-4337 smart contract account
  - Social Recovery usin Web3Auth
  - (TODO) Add verifiable claims such as KYC or ENS to verify ownership of Account Abstraction contract for frontends.
- **Smart Contracts**
  - Self-sovereign ERC-721 developed in-house at Ninfa.io featuring
    - Embedded buy and sell functions including lazy minting (ERC-712)
  - Contract Factory
  - Extensions; burnable, enumerable, metadataURI, creator royalties

## Prerequisites

- [Node.js 18+](http://nodejs.org)
- [Foundry](https://book.getfoundry.sh/getting-started/installation)

## Getting Started

**Step 1:** The easiest way to get started is to clone the repository:

```bash
# Install Node Modules

pnpm i

# Install smart contract libraries

forge install

# Compile Contracts

forge build
```

## Obtaining API Keys

You will need to obtain appropriate credentials (Client ID, Client Secret, API Key, or Username & Password) for API and service provides which you need.

Create a new `.env` file and update the placeholder keys with the newly acquired ones.

```
ANVIL_ACCOUNT_0_PK="0xac0974bec39a17e36ba4a6b4d238ff944bacb478cbed5efcae784d7bf4f2ff80"
ANVIL_MNEMONIC="test test test test test test test test test test test junk"
REACT_APP_PRIV_KEY=""
INFURA_IPFS_PROJECT_ID=""
INFURA_IPFS_PROJECT_SECRET=""
INFURA_API_KEY=""
REACT_APP_INFURA_PROJECT_ID=""
REACT_APP_GOOGLE=""
REACT_APP_WEB3AUTH_CLIENT_ID=""
```

## Initializing the Projecy

### Run Anvil

In a new terminal start the development blockchain

`anvil`

### Run Deployment Script

`forge script script/DeployERC721.s.sol:Anvil --fork-url=localhost -vv --broadcast`

or

`forge script script/DeployERC721.s.sol:Goerli --fork-url=goerli -vv --broadcast`

### Run IPFS script

Run the node script providing as arguments the chain id and the ERC721 contract address, found in
`./broadcast/DeployERC721.s.sol/<chainId>/run-latest.json` under `transactions[0].contractAddress`

`node src/utils/ipfs.mjs <chainId> <deployed_contract_address>`

When using Anvil the contract address will always be the same, as long as the deployment script is run on a fresh Anvil
instance, i.e. the CREATE tx is the first on the local blockchain and the deployer is account[0]

`node src/utils/ipfs.mjs 31337 0x5FbDB2315678afecb367f032d93F642f64180aa3`

### Run Minting Script

`forge script script/Mint.s.sol:Anvil --fork-url=localhost -vv --broadcast`

or

`forge script script/Mint.s.sol:Goerli --fork-url=goerli -vv --broadcast`

This script will iterate each line in `./src/assets/bytes32CIDs.txt` and mint a new token id for each NFT published on
IPFS in the previous step.

## License

The MIT License (MIT)

Copyright (c) 2014-2023 Sahat Yalkabov

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the "Software"), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
