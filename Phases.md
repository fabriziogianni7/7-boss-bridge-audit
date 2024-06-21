
# Phases 

1. understanding what protocol does 
- bridge to L1 to a custom L2
- flow:
    - user deposit token in vault on L1
    - an event is triggered from the vault
    - off chain mechanism pick the event up, parses the event and mint tokens on L2
- security mechanisms:
    - owner of bridge can pause the operations in emergency situations
    - there is a limit of tokens  that can be deposited
    - withdrawals must be approved by a bridge operator
- Launching on ETH mainnet and zkSync
- only L1token  can be bridged
- withdrawals
    - bridge operator is in charge of signing withdrawal(?) requests  submitted by users
    - these requests will be submitted on L2 component (not in the scope)
    - boss bridge will validate the payloads submitted by users, checking that the account submitting the withdrawal has actually deposited on L1
- Roles:
    Bridge owner:
        pause/unpause bridge
        set signers
    Signers
        users who can send a token from L2 to L1
    Vault
        the contract owned by the bridge that hold the tokes
    Users
        call `depositTokensToL2` to send token from L1 to L2

2. scoping contracts to audit 
    ./src/
        #-- L1B ossBridge.sol
        #-- L1Token.sol
        #-- L1Vault.sol
        #-- TokenFactory.sol

        TokenFactory.sol will be deployed on mainnet and zksync
3. run coverage to see where contract is less tested 
```
| File                 | % Lines        | % Statements   | % Branches    | % Funcs       |
|----------------------|----------------|----------------|---------------|---------------|
| src/L1BossBridge.sol | 77.78% (14/18) | 82.61% (19/23) | 83.33% (5/6)  | 71.43% (5/7)  | // cnan be better
| src/L1Token.sol      | 100.00% (1/1)  | 100.00% (1/1)  | 100.00% (0/0) | 100.00% (1/1) |
| src/L1Vault.sol      | 50.00% (1/2)   | 50.00% (1/2)   | 100.00% (0/0) | 50.00% (1/2)  | // just 50%
| src/TokenFactory.sol | 100.00% (4/4)  | 100.00% (4/4)  | 100.00% (0/0) | 66.67% (2/3)  |
| Total                | 80.00% (20/25) | 83.33% (25/30) | 83.33% (5/6)  | 69.23% (9/13) |
```

4. running aderyn and slither 
5. casually reading the code 
6. reading tests
7. understand protocol invariant
8. write tests to find bugs
