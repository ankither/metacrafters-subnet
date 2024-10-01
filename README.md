# Vault and ERC20 Smart Contracts

## Overview

This project contains two Solidity contracts: 

1. **ERC20**: A basic implementation of the ERC20 token standard with minting and burning capabilities.
2. **Vault**: A smart contract that allows users to deposit and withdraw ERC20 tokens in a liquidity vault, minting shares based on the deposit and burning shares upon withdrawal.

---

## Vault Contract

### Description

The `Vault` contract manages deposits and withdrawals of ERC20 tokens in exchange for shares representing a user's stake in the vault. When users deposit tokens, they receive shares proportional to the amount of tokens deposited relative to the total token balance in the vault. When they withdraw tokens, their shares are burned, and they receive an equivalent amount of tokens.

### Key Components

1. **IERC20 Interface**: 
   The `Vault` contract interacts with any token implementing the ERC20 standard using the `IERC20` interface.

2. **_mint Function**: 
   Mints new shares when a user deposits tokens into the vault.

3. **_burn Function**: 
   Burns shares when a user withdraws tokens from the vault.

4. **Deposit Function**: 
   Allows users to deposit tokens into the vault. The number of shares minted is proportional to the user's deposit relative to the total balance of tokens in the vault.

5. **Withdraw Function**: 
   Allows users to withdraw tokens from the vault by burning their shares. The amount of tokens returned is proportional to the shares burned relative to the total supply of shares.

### Functions

- **deposit(uint _amount)**: 
  - Deposits ERC20 tokens into the vault.
  - Mints shares for the depositor based on the vault's total supply and token balance.
  
- **withdraw(uint _shares)**: 
  - Withdraws ERC20 tokens from the vault.
  - Burns the user's shares and transfers the proportional amount of tokens back to the user.

### Mathematical Formulas

1. **Deposit**:
   - When a user deposits tokens, the number of shares minted is calculated using:
     \[
     s = \frac{a \cdot T}{B}
     \]
     Where:
     - \( a \) = amount of tokens deposited.
     - \( T \) = total supply of shares.
     - \( B \) = balance of tokens in the vault before deposit.

2. **Withdraw**:
   - When a user withdraws tokens, the amount of tokens withdrawn is calculated using:
     \[
     a = \frac{s \cdot B}{T}
     \]
     Where:
     - \( a \) = amount of tokens to withdraw.
     - \( s \) = shares to burn.
     - \( B \) = balance of tokens in the vault.
     - \( T \) = total supply of shares.

---

## ERC20 Contract

### Description

This contract implements the basic functionality of an ERC20 token, allowing minting, burning, and token transfers. It also includes the necessary events for `Transfer` and `Approval` per the ERC20 standard.

### Key Components

1. **Mapping of Balances**: 
   Tracks token balances for each user (`balanceOf`).

2. **Mapping of Allowances**: 
   Tracks the amount of tokens an owner has allowed a spender to transfer on their behalf (`allowance`).

3. **Transfer Function**: 
   Allows users to transfer tokens to other addresses.

4. **Approve Function**: 
   Allows users to approve a spender to transfer a specified amount of tokens on their behalf.

5. **TransferFrom Function**: 
   Allows an approved spender to transfer tokens on behalf of the owner.

6. **Mint and Burn**: 
   Allows minting new tokens to a user and burning tokens from a user's balance.

### Functions

- **transfer(address recipient, uint amount)**: 
  - Transfers tokens from the sender's account to the recipient.
  
- **approve(address spender, uint amount)**: 
  - Approves a spender to transfer a specified amount of tokens on behalf of the owner.

- **transferFrom(address sender, address recipient, uint amount)**: 
  - Transfers tokens from one address to another, requiring prior approval.
  
- **mint(uint amount)**: 
  - Mints new tokens to the sender’s account.
  
- **burn(uint amount)**: 
  - Burns tokens from the sender’s account, reducing the total supply.

---

## How to Use

1. **Deploying the Contracts**:
   - Deploy the `ERC20` contract first to create the token.
   - Deploy the `Vault` contract, passing the address of the deployed ERC20 token to its constructor.

2. **Minting Tokens**:
   - Call the `mint` function in the `ERC20` contract to create tokens for a user.

3. **Depositing Tokens in Vault**:
   - Approve the `Vault` contract to spend tokens on behalf of the user using the `approve` function of the ERC20 token.
   - Call the `deposit` function in the `Vault` contract to deposit tokens and mint shares.

4. **Withdrawing Tokens from Vault**:
   - Call the `withdraw` function in the `Vault` contract to burn shares and receive tokens back.

---

## Events

- **Transfer**: 
  - Emitted when tokens are transferred between accounts or minted/burned.
  
- **Approval**: 
  - Emitted when an owner approves a spender to transfer tokens on their behalf.

---

## License

This project is licensed under the MIT License.
