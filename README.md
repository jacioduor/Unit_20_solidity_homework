# Unit 20 - "Looks like we've made our First Contract!-`AssociateProfitSplitter"

![contract](Images/smart-contract.png)

## Background

This is a smart contracts to automate some company finances to make everyone's lives easier, increase transparency, and to make accounting and auditing practically automatic!

I have programed a smart contracts with Solidity called `ProfitSplitter`.There are three sets of the same contract but the requirment for this assinment to do one but if motivated do all. I have chosen to do one- the first one. The smart contracts will:-

* Pay your Associate-level employees quickly and easily.

* Distribute profits to different tiers of employees.

* Distribute company shares for employees in a "deferred equity incentive plan" automatically.

## Files

* [`AssociateProfitSplitter.sol`](Starter-Code/AssociateProfitSplitter.sol) -- Level 1 starter code.

* starter code.

## Building the smart contract:-Level One** `AssociateProfitSplitter` contract. This will accept Ether into the contract and divide the Ether evenly among the associate level employees. This will allow the Human Resources department to pay employees quickly and efficiently.


### Starting your project

I navigated to the [Remix IDE](https://remix.ethereum.org) and created a new contract called `AssociateProfitSplitter.sol` using the starter code for level one above.

While developing and testing your contract,  I used the [Ganache](https://www.trufflesuite.com/ganache) development chain, and point MetaMask to `localhost:8545`, or replace the port with what you have set in your workspace.

### Level One: The `AssociateProfitSplitter` Contract

At the top of my contract, i defined the following `public` variables:

* `employee_one` -- The `address` of the first employee. Maing sure to set this to `payable`.

* `employee_two` -- Another `address payable` that represents the second employee.

* `employee_three` -- The third `address payable` that represents the third employee.

I thereafter created a constructor function that accepts:

* `address payable _one`

* `address payable _two`

* `address payable _three`

Within the constructor, set the employee addresses to equal the parameter values. to  allow me to avoid hardcoding the employee addresses.

Next, I created the following functions:

* `balance` -- I set this function  to `public view returns(uint)`, and  returned the contract's current balance. Since i should always be sending Ether to the beneficiaries, this function should always return `0`. If it does not, the `deposit` function is not handling the remainders properly and should be fixed. 

* `deposit` -- This function should set to `public payable` check, ensuring that only the owner can call the function.

  * In this function, I performed the following steps:

    * Set a `uint amount` to equal `msg.value / 3;` in order to calculate the split value of the Ether.

    * Transfered the `amount` to `employee_one`.

    * Repeated the steps for `employee_two` and `employee_three`.

    * Since `uint` only contains positive whole numbers, and Solidity does not fully support float/decimals, we must deal with a potential remainder at the end of this function since `amount` will discard the remainder during division.

    * Either  I will have `1` or `2` wei leftover, so transfer the `msg.value - amount * 3` back to `msg.sender`. This will re-multiply the `amount` by 3, then subtract it from the `msg.value` to account for any leftover wei, and send it back to Human Resources.

* Nest I created a fallback function using `function() external payable`, to call the `deposit` function from within it. This was to ensure that the logic in `deposit` executes if Ether is sent directly to the contract. This is important to prevent Ether from being locked in the contract since we don't have a `withdraw` function in this use-case.

#### Test the contract

In the `Deploy` tab in Remix, I deployed the contract to my local Ganache chain by connecting to `Injected Web3` and ensuring MetaMask is pointed to `localhost:8545`.

I filled in the constructor parameters with my designated `employee` addresses.
This is the screenshot of the deployed contract

![Remix Testing](Images/remix-deploy-1.png)


I then tested the `deposit` function by sending the values of 1 eith to the three accounts Keeping an eye on the `employee` balances as I  sent different amounts of Ether to the contract and ensure the logic is executing properly. Below is the screen shot of My MetaMax confirming the Transfers 

![MetaMax](Images/metamsk-confirm.png)


Below is the Ganache screenshot confirming the movement of the eth in the account addresses used- from 100 to 101

![Ganache ](Images/ganache-transfer.png)

## Submission

I Created this  `README.md`  and uploaded to the  Github repository and provided the testnet address for others to interact with the contract.

