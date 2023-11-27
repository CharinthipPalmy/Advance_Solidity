# Unit 21: Martian Token Crowdsale

![alt=""](pics/image1.jpeg)

## Background

After waiting for years and passing several tests, the Martian Aerospace Agency selected you to become part of the first human colony on Mars. As a prominent fintech professional, they chose you to lead a project developing a monetary system for the new Mars colony. You decided to base this new system on blockchain technology and to define a new cryptocurrency named **KaseiCoin**. (Kasei means Mars in Japanese.)

KaseiCoin will be a fungible token that’s ERC-20 compliant. You’ll launch a crowdsale that will allow people who are moving to Mars to convert their earthling money to KaseiCoin.

## Files

Download the following files to help you get started:

[KaseiCoin.sol](./Starter_Code/KaseiCoin.sol)

[KaseiCoinCrowdsale.sol](./Starter_Code/KaseiCoinCrowdsale.com)

## Instructions

The steps for this assignment are divided into the following subsections:

1. Create the KaseiCoin Token Contract

2. Create the KaseiCoin Crowdsale Contract

3. Create the KaseiCoin Deployer Contract

4. Deploy and Test the Crowdsale on a Local Blockchain

5. Optional: Extend the Crowdsale Contract by Using OpenZeppelin

    > **Note:** You can choose whether to complete the optional section. It’s designed to further your professional growth and development but won’t be graded as part of this assignment. If you choose to complete this section, you’ll use OpenZeppelin to extend the functionality of your crowdsale contract by adding time restrictions, refund capabilities, and a cap for the number of tokens that can be created. If you have any questions about how to complete the optional section, please reach out to your instructional team.

Note that the provided starter files for this homework assignment contain a `pragma` statement for Solidity version 0.5.0. You’ll use the starter files to complete the steps in the subsections.

In the subsections, you’ll create a fungible token that’s ERC-20 compliant. This token will be minted by using a `Crowdsale` contract from the OpenZeppelin Solidity library.

The crowdsale contract that you create will manage the entire crowdsale process. This process will allow users to send ether to the contract and receive KaseiCoin tokens, or **KAI**, in return. Your contract will automatically mint the tokens and distribute them to a buyer in one transaction.

Note that you’ll record a short video or animated GIF or take several screenshots that show the deployed contract in action.

In the `README.md` file of your GitHub repository for this homework assignment, you’ll create a section named Evaluation Evidence. In this section, you’ll share screenshots of your work from each subsection of the assignment.

### Step 1: Create the KaseiCoin Token Contract

In this subsection, you’ll create a smart contract that defines KaseiCoin as an ERC-20 token. To do so, complete the following steps:

1. Import the provided `KaseiCoin.sol` starter file into the Remix IDE.

2. Import the following contracts from the OpenZeppelin library:

    * `ERC20`

    * `ERC20Detailed`

    * `ERC20Mintable`

3. Define a contract for the KaseiCoin token, and name it `KaseiCoin`. Have the contract inherit the three contracts that you just imported from OpenZeppelin.

#### contract KaseiCoin is ERC20, ERC20Detailed, ERC20Mintable {

4. Inside your `KaseiCoin` contract, add a constructor with the following parameters: `name`, `symbol`, and `initial_supply`.

####     constructor(
####        string memory name,
####        string memory symbol,
####        uint initial_supply
####    )
5. As part of your constructor definition, add a call to the constructor of the `ERC20Detailed` contract, passing the parameters `name`, `symbol`, and `18`. (Recall that 18 is the value for the `decimals` parameter.)

####    ERC20Detailed(name, symbol, 18) public {
####        _mint(msg.sender, initial_supply);
####    }
#### }

6. Compile the contract by using compiler version 0.5.0.

7. Check for any errors, and debug them as needed.

8. Take a screenshot of the successful compilation of the contract, and add it to the Evaluation Evidence section of the `README.md` file for your GitHub repository.
![images](pics/image6.jpeg)

### Step 2: Create the KaseiCoin Crowdsale Contract

In this subsection, you’ll define the KaseiCoin crowdsale contract. To do so, complete the following steps:

1. Import the provided `KaseiCoinCrowdsale.sol` starter code into the Remix IDE.

2. Have this contract inherit the following OpenZeppelin contracts:

    * `Crowdsale`

    * `MintedCrowdsale`
#### contract KaseiCoinCrowdsale is Crowdsale, MintedCrowdsale {

3. In the `KaisenCoinCrowdsale` constructor, provide parameters for all the features of your crowdsale, such as `rate`, `wallet` (where to deposit the funds that the token raises), and `token`. Configure these parameters as you want for your KaseiCoin token.
#### // Provide parameters for all of the features of your crowdsale, such as the `rate`, `wallet` for fundraising, and `token`.
####     constructor(
####         uint256 rate, 
####         address payable wallet, 
####         KaseiCoin token

####     ) public
####         Crowdsale(rate, wallet, token)

####     {
####         // constructor can stay empty
####     }
#### }
4. Compile the contract by using compiler version 0.5.0.

5. Check for any errors, and debug them as needed.

6. Take a screenshot of the successful compilation of the contract, and add it to the Evaluation Evidence section of the `README.md` file for your GitHub repository.
![images](pics/image7.jpeg)
### Step 3: Create the KaseiCoin Deployer Contract

In this subsection, you’ll create the KaseiCoin deployer contract. Start by uncommenting the `KaseiCoinCrowdsaleDeployer` contract in the provided `KaseiCoinCrowdsale.sol` starter code.

#### contract KaseiCoinCrowdsaleDeployer {

Next, in the `KaseiCoinCrowdsaleDeployer` contract, you’ll add variables to store the addresses of the `KaseiCoin` and `KaseiCoinCrowdsale` contracts, which this contract will deploy. Finally, you’ll complete the `KaseiCoinCrowdsaleDeployer` contract. To do so, complete the following steps:

1. Create an `address public` variable named `kasei_token_address`, which will store the `KaseiCoin` address once that contract has been deployed.

#### address public kasei_token_address;
2. Create an `address public` variable named `kasei_crowdsale_address`, which will store the `KaseiCoinCrowdsale` address once that contract has been deployed.

#### address public kasei_crowdsale_address;
3. Add the following parameters to the constructor for the `KaseiCoinCrowdsaleDeployer` contract: `name`, `symbol`, and `wallet`.
#### constructor(
####        string memory name,
####        string memory symbol,
####        uint256 rate,
####        address payable wallet
####    )
####        public
####    {
4. Inside of the constructor body (that is, between the braces), complete the following steps:

    * Create a new instance of the `KaseiCoinToken` contract.
#### KaseiCoin token = new KaseiCoin(name, symbol, 0);
    * Assign the address of the KaseiCoin token contract to the `kasei_token_address` variable. (This will allow you to easily fetch the token's address later.)

#### kasei_token_address = address(token);
    * Create a new instance of the `KaseiCoinCrowdsale` contract by using the following parameters:

      * The `rate` parameter: Set `rate` equal to 1 to maintain parity with ether.

      * The `wallet` parameter: Pass in `wallet` from the main constructor. This is the wallet that will get paid all the ether that the crowdsale contract raises.

      * The `token` parameter: Make this the `token` variable where `KaseiCoin` is stored.
#### KaseiCoinCrowdsale kasei_coin_crowdsale = new KaseiCoinCrowdsale(rate, wallet, token);
    * Assign the address of the KaseiCoin crowdsale contract to the `kasei_crowdsale_address` variable. (This will allow you to easily fetch the crowdsale’s address later.)
#### kasei_crowdsale_address = address(kasei_coin_crowdsale);
    * Set the `KaseiCoinCrowdsale` contract as a minter.
#### token.addMinter(kasei_crowdsale_address);
    * Have the `KaseiCoinCrowdsaleDeployer` renounce its minter role.
####    token.renounceMinter();
####    }
#### }

5. Compile the contract by using compiler version 0.5.0.

6. Check for any errors, and debug them as needed.

7. Take a screenshot of the successful compilation of the contract, and add it to the Evaluation Evidence section of the `README.md` file for your Git repository.
![images](pics/image8.jpeg)
### Step 4: Deploy and Test the Crowdsale on a Local Blockchain

In this subsection, you’ll deploy the crowdsale to a local blockchain. You’ll then perform a real-world, preproduction test of your crowdsale. To do so, complete the following steps:

> **Important:** Record a short video or take screenshots that illustrate the following steps as evidence of your deployed crowdsale contract.

1. Deploy the crowdsale to a local blockchain by using Remix, MetaMask, and Ganache.
![images](pics/image2.jpeg)
![images](pics/image3.jpeg)
2. Test the functionality of the crowdsale by using test accounts to buy new tokens and then checking the balances of those accounts.

![images](pics/image4.jpeg)
3. Review the total supply of minted tokens and the amount of wei that the crowdsale contract has raised.
![images](pics/image5.jpeg)



---

© 2022 edX Boot Camps LLC. Confidential and Proprietary. All Rights Reserved.
