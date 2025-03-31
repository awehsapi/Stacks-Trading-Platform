# Stacks-Trading-Platform - Bitcoin Options Trading Contract V2

## Overview
Bitcoin Options Trading Contract V2 is a decentralized smart contract that enables peer-to-peer options trading with internal Bitcoin (BTC) tracking. The contract supports both CALL and PUT options, allowing users to create, purchase, and exercise options without intermediaries. It also includes an internal BTC balance system and price oracle functionality.

## Features
- **Decentralized Options Trading**: Peer-to-peer trading without centralized control.
- **CALL and PUT Options**: Supports both option types for flexible trading strategies.
- **BTC Balance Management**: Users can deposit, withdraw, and transfer BTC within the contract.
- **Exercise Options**: Users can execute options based on real-time market conditions.
- **User Portfolio Management**: Tracks user-created and purchased options.
- **Oracle Price Feeds**: Admin-controlled BTC price oracle for accurate market data.

## Smart Contract Components

### Constants
The contract defines several error codes and option types:
- **Error Codes**: ERR-EXPIRED, ERR-INVALID-AMOUNT, ERR-UNAUTHORIZED, etc.
- **Option Types**: CALL (1), PUT (2)

### Data Structures
- **BTCBalances**: Maps user principals to their BTC balance.
- **Options**: Stores all option contracts, including creator, buyer, strike price, premium, expiry, BTC amount, and status.
- **UserOptions**: Tracks options created and purchased by each user.
- **next-option-id**: Tracks the next available option ID.
- **oracle-price**: Stores the current BTC price set by the contract owner.

### Core Functionalities

#### BTC Balance Management
- **deposit-btc(amount)**: Deposits BTC into the contract.
- **withdraw-btc(amount)**: Withdraws BTC from the contract.
- **transfer-btc(from, to, amount)**: Transfers BTC between users within the contract.

#### Option Management
- **create-option(option-type, strike-price, premium, expiry, btc-amount)**: Allows users to create an option contract.
- **exercise-option(option-id)**: Enables the buyer to execute an option before expiry.
- **exercise-call(option, holder)**: Executes a CALL option by transferring the strike price.
- **exercise-put(option, holder)**: Executes a PUT option by transferring BTC at the strike price.
- **update-user-options(user, option-id, is-creator)**: Updates the user's portfolio after creating or purchasing an option.

#### Read-Only Functions
- **get-option(option-id)**: Retrieves details of an option.
- **get-btc-balance(holder)**: Fetches a user's BTC balance.
- **get-user-options(user)**: Gets all options associated with a user.
- **get-btc-price()**: Returns the current BTC price from the oracle.

#### Oracle Functions
- **set-btc-price(price)**: Allows the contract owner to set the BTC price.

## Usage

### Depositing BTC
Users can deposit BTC into the contract for trading purposes.
```clojure
(deposit-btc u1000) ;; Deposits 1000 satoshis
```

### Creating an Option
A user can create a CALL or PUT option, specifying the strike price, premium, expiry, and BTC amount.
```clojure
(create-option u1 u50000 u1000 u200000 u10) ;; Creates a CALL option
```

### Exercising an Option
A buyer can exercise an option before expiry.
```clojure
(exercise-option u1) ;; Exercises option ID 1
```

### Withdrawing BTC
Users can withdraw available BTC from their balance.
```clojure
(withdraw-btc u500) ;; Withdraws 500 satoshis
```

### Checking Balances and Options
```clojure
(get-btc-balance tx-sender) ;; Fetch BTC balance
(get-user-options tx-sender) ;; Retrieve user options
(get-option u1) ;; View option ID 1 details
```

### Updating BTC Price (Admin Only)
```clojure
(set-btc-price u60000) ;; Updates BTC price to 60,000 satoshis
```

## Security Considerations
- **Access Control**: Only the contract owner can update the BTC price.
- **Balance Checks**: Ensures users have sufficient funds before transactions.
- **Expiration Handling**: Prevents execution of expired options.

## Future Enhancements
- **Decentralized Price Feeds**: Implement external oracle integrations.
- **Automated Settlement**: Reduce manual option execution steps.
- **Enhanced Liquidity Mechanisms**: Improve market participation.

## License
This smart contract is open-source and free to use under an MIT license.

