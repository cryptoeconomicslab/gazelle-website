---
id: Plasma_Light_Client
title: Plasma Light Client API
sidebar_label: Plasma Light Client
description: Check out Gazelle's API reference to set up a Plasma Light Client without hassles.
---

## deposit

▸ **deposit**(`amount`: number, `tokenContractAddress`: string): _Promise‹void›_

Deposit given amount of token to corresponding deposit contract.
this method calls `approve` method of ERC20 contract and `deposit` method
of Deposit contract.

**Parameters:**

| Name                   | Type   | Description                            |
| ---------------------- | ------ | -------------------------------------- |
| `amount`               | number | amount to deposit                      |
| `tokenContractAddress` | string | token contract address to deposit into |

**Returns:** _Promise‹void›_

---

## transfer

▸ **transfer**(`amount`: number, `tokenContractAddressString`: string, `toAddress`: string): _Promise‹void›_

transfer token to new owner. throw if given invalid inputs.

**Parameters:**

| Name                         | Type   | Description        |
| ---------------------------- | ------ | ------------------ |
| `amount`                     | number | amount to transfer |
| `tokenContractAddressString` | string | -                  |
| `toAddress`                  | string | -                  |

**Returns:** _Promise‹void›_

---

## startWithdrawal

▸ **startWithdrawal**(`amount`: number, `tokenContractAddress`: string): _Promise‹void›_

Withdrawal process starts from calling this method.
Given amount and tokenContractAddress, checks if client has sufficient token amount.
If client has sufficient amount, create exitProperty from stateUpdates this client owns,
calls `claimProperty` method on UniversalAdjudicationContract. Store the property in exitList.
User can call `completeWithdrawal` to withdraw actual token after the exitProperty is decided to true on-chain.

**Parameters:**

| Name                   | Type   | Description                    |
| ---------------------- | ------ | ------------------------------ |
| `amount`               | number | amount to exit                 |
| `tokenContractAddress` | string | token contract address to exit |

**Returns:** _Promise‹void›_

---

## completeWithdrawal

▸ **completeWithdrawal**(`exit`: Exit): _Promise‹void›_

Given exit instance, finalize exit to withdraw token from deposit contract.
Client checks if the exitProperty of the exit instance is decided by calling `isDecided` method
of UniversalAdjudicationContract. If the property claim have not been decided yet, call `decideClaimToTrue`.
If the exitProperty had been decided to true, call `finalizeExit` method of corresponding payout contract.

**Parameters:**

| Name   | Type | Description             |
| ------ | ---- | ----------------------- |
| `exit` | Exit | Exit object to finalize |

**Returns:** _Promise‹void›_

---

## getBalance

▸ **getBalance**(): _Promise‹Array‹object››_

Get current balance of tokens in plasma.
All ERC20 tokens including Peth registered by `registerCustomToken` method or `registerToken` method are included.

**Returns:** _Promise‹Array‹object››_

---

## getPendingWithdrawals

▸ **getPendingWithdrawals**(): _Promise‹Exit[]›_

Get pending exit list

**Returns:** _Promise‹Exit[]›_

---

## registerToken

▸ **registerToken**(`erc20ContractAddress`: string, `depositContractAddress`: string): _void_

register ERC20 token. use default ERC20 contract wrapper.

**Parameters:**

| Name                     | Type   | Description                                               |
| ------------------------ | ------ | --------------------------------------------------------- |
| `erc20ContractAddress`   | string | ERC20 token address to register                           |
| `depositContractAddress` | string | deposit contract address connecting to tokenAddress above |

**Returns:** _void_
