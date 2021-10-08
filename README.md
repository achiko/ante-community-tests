# ante-community-tests

Please feel free to join our Discord to bounce ideas and discuss various ideas with the community and developers!

Website: [ante.finance](https://www.ante.finance/)  
Twitter: [AnteFinance](https://twitter.com/AnteFinance)  
Discord: [Ante Finance](https://discord.gg/yaJthzNdNG)  

**IMPORTANT - We're incredibly excited by the enthusiasm the community is showing towards writing Ante Tests for their favorite protocols. We're still working on making the test deployment process as seamless and user-friendly as possible.**

**To help with this, we ask that you open a PR against this repo and get feedback from our community before deploying your ante test on-chain**

---

## If you want to contribute to the community repository see the instructions below

### Installation

Install Node and NPM ([Instructions](https://docs.npmjs.com/downloading-and-installing-node-js-and-npm))

```
Make sure to use Node version 14 or higher and NPM version 6 or higher
```

Fork the ante-community-tests repository by clicking the `Fork` button in the upper right hand corner of this page, then clone your fork to your local machine with

```
git clone git@github.com:[YOUR_GITHUB_USERNAME]/ante-community-tests.git
```

Install all required packages

```
npm install --save-dev
```

### Configure the app

- copy [`.env.example`](./.env.example) to [`.env`](./.env) and fill in your Infura API Key, Alchemy API Key, the mainnet private key for your desired mainnet deployment address, and memnonic phrase. The first address generated by this mnemonic is used to deploy contracts from this repo to testnet and mainnet
- If you do not have a mnemonic you can use `test test test test test test test test test test test junk` 
- An Alchemy API key is required to run the testing suite and can be obtained for free at [alchemy.com](https://www.alchemy.com/)
- An Infura API key can be obtained for free at [infura.io](https://infura.io/)


### Write your ante test

Write an ante test for your desired protocol and put it in a file called `./contracts/[PROTOCOL_NAME]/[YOUR_TEST_NAME].sol`. For more information on writing Ante Tests, see our [docs](https://docs.ante.finance/). Also stop by our [Discord](https://discord.gg/yaJthzNdNG) and ask questions!


**(Optional)** you can also write some unit tests that check whether or not your AnteTest works. These unit tests should be placed in a file called `./test/[PROTOCOL_NAME]/[YOUR_TEST_NAME].spec.ts`

Then run the following command:

```
npm run test
```

This command runs your unit tests against a forked version of the ethereum mainnet. Once you've verified everything is working properly, it's time to deploy your ante test to testnet and then mainnet!

**If you are trying to run the testing suite with `npx hardhat test`, you must run `npx hardhat typechain` first to avoid an error where hardhat cannot find the typechain directory**

### Finally, push your code to your own github repo and create a pull request against this repo

Show off what you've built in our [discord](https://discord.gg/yaJthzNdNG) or tweet your PR at us on [twitter](https://twitter.com/antefinance)! **VERY IMPORTANT** - Make sure to get feedback from our community before deploying your Ante Test to main-net! Testing and feedback are the best way to catch bugs early (and avoid wasting gas).


# Beginner-friendly Setup Tutorial

_The following has been provided by [@waynebruce0x](https://github.com/waynebruce0x) and provides a beginner-friendly introduction to setting up a Hardhat development environment and writing an Ante Test from scratch:_

## Getting Started Writing Ante Tests
There are many different tools and methods you can use to develop Ante Tests. In this guide we’ll use
Hardhat and Alchemy, however feel free to adapt this guide to suit your favourite Ethereum development
tools. Hardhat is an environment for developing, testing and deploying smart contracts, and Alchemy is
an Ethereum node service which allows us to interact with projects already on the blockchain.

## Installing A Recent Version of Node.js
First we’ll need a recent version of Node.js, so we can run JavaScript code (which Hardhat is build on
top of). Hardhat have an excellent guide on their website for installing Node.js. This is part of their
Hardhat tutorial which we would recommend to anyone new to Ethereum development.
https://hardhat.org/tutorial/setting-up-the-environment.html

## Creating Your Ante Test Project
Next we’re going to create a new project folder called AnteTest, and change your terminal directory to
this folder so that any future commands run inside the AnteTest folder
```
mkdir AnteTest && cd AnteTest
```
Then create a new package.json file for your project, install hardhat, and run it. If these steps are
successful you’ll see ‘welcome to Hardhat’ printed in your terminal. Use your arrow keys to select ‘Create
an empty hardhat.config.js’
```
npm init -y
npm install --save-dev hardhat
npx hardhat
```
create an empty hardhat.config.js
Great, so now we have your empty Hardhat project ready and waiting. Next we’ll install some plugins to
make things easier. Openzeppelin have a bunch of libraries useful for Ethereum development. We’re just
going to install hardhat-upgrades and contracts. Nomiclabs’ ethers library makes it easier for us to
interact with the Ethereum blockchain.
```
npm install --save-dev @openzeppelin/hardhat-upgrades
npm install --save-dev @openzeppelin/contracts
npm install --save-dev @nomiclabs/hardhat-ethers ethers # peer dependencies
```

## Creating An Alchemy App
sign up to Alchemy at https://www.alchemy.com/. Once you have made a project / app you’ll be given a
unique ‘integrate with alchemy’ URL. Keep this safe! This will allow us to fork the current state of the
Ethereum blockchain, allowing us to interact with projects that have already been deployed (like AAVE,
Uniswap, WBTC etc).

## Configuring Your Ante Test Project
At this point it’s a good idea to open up the AnteTest project in your IDE. You should be able to see a
`hardhat.config.js` file, open it up because we’re going to edit it’s contents. We’re going to add
requirements for two of the plugins we just installed, and give your project details of your Alchemy node.
Clear your `hardhat.config.js` file, then copy and paste the code below into it, where "[ALCHEMYURL]" is
the http address of your Alchemy node. Make `hardhat.config.js` this:
```
require("@nomiclabs/hardhat-ethers");
require("@openzeppelin/hardhat-upgrades");
/**
* @type import('hardhat/config').HardhatUserConfig
*/
module.exports = {
  solidity: "[YOUR DESIRED VERSION]",
  networks: {
    hardhat: {
      forking: {
        url: "[ALCHEMYURL]",
      }
    }
  }
};
```

## Adding The Ante Interfaces
Make a new folder in the project called contracts, and inside that, make another folder called interfaces.
Copy the IAnteTest interface and the AnteTest abstract class into this interfaces folder (you can find them
here https://docs.ante.finance/antev05/tutorials/write-an-ante-test/iantetest.sol-and-antetest.sol)

## Writing Your Ante Test
For this step you need to get creative. There are some examples in the Ante docs that you can use as
inspiration. Google search is great for getting ideas and debugging your contract, and if you get stuck
you can always ask us questions in the Ante Discord server!

Put your test in the contracts folder when it’s finished. Then make a new folder called ‘scripts’, with a file
‘deploy.js’ inside it. You’ll also have to write the deployment script yourself (some help can be found here
https://hardhat.org/tutorial/deploying-to-a-live-network.html).


## Putting It All Together
Now you’re ready to check your Ante Test works as you expected! We’re going to run a fork of the
current Ethereum mainnet. This means we can interact with the blockchain without losing any real
money. This step is important because it lets us check that the Ante Test works without any issues
(because even the best devs tests often don’t work first time!).
Start up your local hardhat node

```npx hardhat node```

Then in a seperate terminal window, also in the AnteTest directory, compile your smart contracts, and
deploy them to the Ethereum fork.

```
npx hardhat compile
npx hardhat run scripts/deploy.js --network localhost
```


