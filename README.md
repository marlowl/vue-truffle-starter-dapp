# Vue truffle starter dApp

<p align="center">		
  <img src="https://cdn-images-1.medium.com/max/1200/1*F1LChP2_EbsSPh4OPaJ7xA.png">		
 </p>
 
This project was generated with [vue-cli](https://github.com/vuejs/vue-cli) version 3.2.1

An Vue [truffle](https://github.com/trufflesuite/truffle) starter dApp. Write, compile & deploy smart contracts for Ethereum.

## Demo
Update a value of a smart contract with your Ethereum wallet address

![](screenshot.gif)

### Part 1 - Ganache and Truffle
Both of these tools are required before moving forward, and be sure you're connected to an Ethereum client before running the commands below.
`npm install -g truffle ganache-cli` to run a local blockchain RPC server. Simply run `ganache-cli` to start Ganache

1. to compile your contracts `truffle compile` 
2  to deploy those contracts to the network`truffle migrate --network ropsten`

### Part 2 - Install dependencies
1. `git clone https://github.com/marlowl/vue-truffle-starter-dapp/`
2. `npm install`
3. `cd vue`
4. `npm install`

### Part 3 - Update .env files
1. In the root:
`MNEMONIC= "your ganache MNEMONIC"`
`INFURA_API_KEY="your infura key"`

2. In the vue folder:
`VUE_APP_ETHADDRESS="your eth address"`

## Run
Run `npm run serve` to start a dev server 

## Build
Run `npm run build` to build the project for a production build

## Technologies & Languages Used
1. Vue (Typescript/Javascript)
2. Truffle (Solidity)
3. Ganache

