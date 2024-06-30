# GamerToken Smart Contract

## Overview

The `GamerToken` smart contract is a simple ERC20-like token implemented in Solidity. This token is designed to manage a custom cryptocurrency called `GAMER` (symbol: `GMR`). The contract owner can mint and burn tokens, and users can transfer tokens between accounts and redeem tokens for game items.

## Contract Details

### Variables

- `totalSupply`: The total supply of `GMR` tokens.
- `owner`: The address of the contract owner.
- `name`: The name of the token (`GAMER`).
- `symbol`: The symbol of the token (`GMR`).
- `decimalUnits`: The number of decimal places the token uses (18).

### Mappings

- `accountBalances`: Maps an address to its token balance.

### Constructor

The constructor sets the contract owner to the address that deploys the contract.

### Functions

#### `mintTokens(address recipient, uint256 amount)`

This function allows the contract owner to mint new tokens.

- **Parameters**:
  - `recipient`: The address to receive the minted tokens.
  - `amount`: The number of tokens to mint.
- **Requirements**:
  - Only the contract owner can call this function.
  - The `amount` must be greater than 0.
- **Behavior**:
  - Increases the balance of the `recipient` by `amount`.
  - Increases the `totalSupply` by `amount`.

#### `burnTokens(address account, uint256 amount)`

This function allows the burning of tokens from a specified account.

- **Parameters**:
  - `account`: The address from which to burn the tokens.
  - `amount`: The number of tokens to burn.
- **Requirements**:
  - The `amount` must not exceed the balance of the `account`.
- **Behavior**:
  - Decreases the balance of the `account` by `amount`.
  - Decreases the `totalSupply` by `amount`.

#### `transferTokens(address recipient, uint256 amount)`

This function allows a user to transfer tokens to another account.

- **Parameters**:
  - `recipient`: The address to receive the tokens.
  - `amount`: The number of tokens to transfer.
- **Requirements**:
  - The `amount` must not exceed the sender's balance.
  - The `recipient` must not be the zero address.
- **Behavior**:
  - Decreases the balance of the sender by `amount`.
  - Increases the balance of the `recipient` by `amount`.

#### `redeemTokens(address user, uint256 amount, uint256 gameItem)`

This function allows a user to redeem tokens for game items.

- **Parameters**:
  - `user`: The address of the user redeeming the tokens.
  - `amount`: The number of tokens to redeem.
  - `gameItem`: The ID of the game item to redeem.
- **Requirements**:
  - The `amount` must not exceed the user's balance.
  - The `gameItem` must be valid (1, 2, or 3).
  - Different game items have different token requirements:
    - Game Item 1 requires at least 50 tokens.
    - Game Item 2 requires at least 100 tokens.
    - Game Item 3 requires at least 200 tokens.
- **Behavior**:
  - Calls the `burnTokens` function to burn the tokens from the `user`'s balance.

## Usage

### Deployment

Deploy the `GamerToken` contract using any Ethereum-compatible development environment. The constructor does not take any parameters and sets the deploying address as the contract owner.

### Minting Tokens

The contract owner can mint tokens by calling the `mintTokens` function with the recipient's address and the amount to mint.

### Burning Tokens

Any user can burn their own tokens by calling the `burnTokens` function with their address and the amount to burn.

### Transferring Tokens

Users can transfer tokens to another address by calling the `transferTokens` function with the recipient's address and the amount to transfer.

### Redeeming Tokens

Users can redeem tokens for game items by calling the `redeemTokens` function with their address, the amount of tokens to redeem, and the game item ID.

## Security Considerations

- Only the contract owner can mint new tokens.
- Users must have sufficient balance to transfer or burn tokens.
- Redeeming tokens for game items requires meeting specific token thresholds.

## License

This project is licensed under the MIT License.
