# Celo Truffle Box

**Mandatory:** Make sure that you have the [Yarn package manager](https://yarnpkg.com/) and [Truffle](https://www.trufflesuite.com/truffle) installed, then in a new project directory run

```bash
$ truffle unbox critesjosh/celo-dappkit
``` 

This [Truffle Box](https://www.trufflesuite.com/boxes) will help you get started building a mobile dapp using Celo and React Native in Javascript. We will build a simple React Native application that we can use to read and update a contract on the Alfajores test network.

The project smart contracts and configuration are in the root directory. The React Native front end is in the `/client` directory. Once you download the box, run 

```bash
$ yarn       # install depenedncies
$ cd client  # move into the client directory
$ yarn       # install front end dependencies
```

This Truffle box uses React Native and [Expo](https://expo.io/) for developing a mobile first Celo blockchain experience. You will also need Expo installed globally on your machine. Install it with:

```bash
$ yarn global add expo-cli
```

## Mobile Dependencies

You will need the Expo app installed on your development mobile device or emulator ([iOS](https://apps.apple.com/app/apple-store/id982107779) or [Android](https://play.google.com/store/apps/details?id=host.exp.exponent&referrer=www)). 

You will also need the [Celo Wallet](https://celo.org/developers/wallet) on your mobile device (or emulator) to sign transactions. The app may automatically connect to a HelloWorld contract that has already been deployed to the testnet, or you may have to deploy your own (details below).

## Smart contract development

The project comes with a Hello World example contract in the root contracts directory. 

The box is also configured to deploy Solidity smart contracts to the Alfajores test network. You will need test network funds to deploy your own contract. 

In the project root run

```bash
$ yarn account
```

to create a new account for development. The new account address will be printed in the console. This script will generate a private key for you and store it in `/.secret`. If you need to print the account info again, run `$ yarn account` again. It will not create a new account, it will read the saved private key and print the corresponding account address. 

Truffle will read this private key for contract deployments. 

Copy your account address and paste it in to the [Alfajores faucet](https://celo.org/developers/faucet) to fund your account.

You can migrate the `HelloWorld.sol` contract to the alfajores test network with

```bash
$ truffle migrate --network alfajores
```

You should deploy the `HelloWorld.sol` contract to work through the exercise. You can deploy it using the remote node specified in `truffle-config.js`. You may get an error about connecting to a running RPC client. If you run into the error, trying running `truffle migrate --network alfajores` again. A successful deployment should print something like the following:

```
Joshs-MacBook-Pro-2:untitled folder joshcrites$ truffle migrate --network alfajores

Compiling your contracts...
===========================
> Everything is up to date, there is nothing to compile.


Starting migrations...
======================
> Network name:    'alfajores'
> Network id:      44786
> Block gas limit: 0x1312d00


1_initial_migration.js
======================

   Deploying 'Migrations'
   ----------------------
   > transaction hash:    0x8a7d5f323ef9e356407566ded4d191e3b68b0ba579c5a7b920e5dea3936bb101
   > Blocks: 0            Seconds: 4
   > contract address:    0x6363f95B5dDe5bbb1A73dbdc752036e105769207
   > block number:        587188
   > block timestamp:     1583779418
   > account:             0x0ac6eDb733EAB57f8fa6c0F8678de0b9ef950bc6
   > balance:             4.98552399999999992
   > gas used:            188419
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.00376838 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00376838 ETH


2_deploy_contracts.js
=====================

   Deploying 'HelloWorld'
   ----------------------
   > transaction hash:    0xb48d8f2da01f49b6ebe3dd2391b289c735afd2ec1b57902a5bd3958c4b5773b3
   > Blocks: 1            Seconds: 4
   > contract address:    0xD9BBC1c3C76bd285C33de5Df4b987369EC66DC56
   > block number:        587190
   > block timestamp:     1583779428
   > account:             0x0ac6eDb733EAB57f8fa6c0F8678de0b9ef950bc6
   > balance:             4.979126059999999888
   > gas used:            277896
   > gas price:           20 gwei
   > value sent:          0 ETH
   > total cost:          0.00555792 ETH


   > Saving migration to chain.
   > Saving artifacts
   -------------------------------------
   > Total cost:          0.00555792 ETH


Summary
=======
> Total deployments:   2
> Final cost:          0.0093263 ETH
```

Since we are developing this on the public Alfajores test network, we can view all the accounts, contracts and transactions on the [public block explorer](https://alfajores-blockscout.celo-testnet.org/).

You can look up the contract deployment transaction on the Alfajores block explorer via the transaction hash, [https://alfajores-blockscout.celo-testnet.org/tx/0xb48d8f2da01f49b6ebe3dd2391b289c735afd2ec1b57902a5bd3958c4b5773b3](https://alfajores-blockscout.celo-testnet.org/tx/0xb48d8f2da01f49b6ebe3dd2391b289c735afd2ec1b57902a5bd3958c4b5773b3) in this case.

Truffle will save the deployment information to the Truffle artifact located at `client/contracts/HelloWorld.json`. You will use this deployment information to connect your React Native application to the correct contract.

## Developing the mobile application

Keep in mind that you will need a version of the Celo Wallet installed on the mobile device with which you are developing the application. The Celo Wallet is the private key management software that the user will sign transactions with. 

You can install the Celo wallet on your physical device with an invite code [here.](https://celo.org/developers/wallet) 

You can build a the latest version of the Celo Wallet and find instructions on running a development build [here.](https://github.com/celo-org/celo-monorepo/tree/master/packages/mobile) 

Once you have a device with the Celo wallet installed, you can start working on your application. 

For the purposes of introduction, we have added some code to you get you started located in App.js in the `client` directory.

### Application development with Expo

In this project, the React Native application lives in the `client` directory. `cd` into the client directory and run `$ yarn` to install the dependencies. 

[Expo](https://expo.io/) is a tool that makes developing React Native applications much easier. We will be using Expo for easy setup.

Install it with:
```
$ npm install expo-cli --global
```

You can start the application with
```
$ expo start
```

You can use your physical mobile device or an emulator to develop apps with Expo. If you want to use your physical device, you will have to [install the Expo app on your device.](https://expo.io/learn)

Make sure the Celo Wallet app is open on your device when you are using your dapp. Your dapp will be requesting information from the Celo Wallet.

### Using an emulator

You can find more information about running and Android emulator [here.](https://developer.android.com/studio/run/emulator-commandline)

## Celo Dapp Examples

[Celo Savings Circle](https://github.com/celo-org/savings-circle-demo)

## Wrapping up

You should now have the necessary skills to get started with developing mobile applications on Celo.

This is not a comprehensive tutorial for Celo's features and capabilities. 

Please [see our documentation](https://docs.celo.org/) for more info and feel free to [connect with us on Discord](https://discord.gg/745Qntv) if you need any help!
