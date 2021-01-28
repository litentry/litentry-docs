# Runtime

Github Repository: [https://github.com/litentry/litentry-node](https://github.com/litentry/litentry-node)

There are two pallets from litentry both account-linker and offchain-worker.

[https://github.com/litentry/litentry-node/blob/develop/pallets/account-linker/src/lib.rs](https://github.com/litentry/litentry-node/blob/develop/pallets/account-linker/src/lib.rs)

[https://github.com/litentry/litentry-node/blob/develop/pallets/offchain-worker/src/lib.rs](https://github.com/litentry/litentry-node/blob/develop/pallets/offchain-worker/src/lib.rs)

### Abstract

The identity runtime protocol link the all cross chain accounts to make an unique Litentry Identity. After accounts linked, Litentry user can trigger the asset claim via transaction. Litentry offchain worker will query your assets in other blockchain network, generate asset prove on-chain. Any Defi or other Dapp can use the information for their service:

1. Account Linking: Litentry user sign the specific data with private key.

2. Asset Claim: Litentry user ask runtime to query its asset and generate prove.

3. Defi or other Dapp: Use the Litentry ID and its assets prove for their service. 

### Stakeholders
1. Litentry user: They register into Litentry network, can get the token incentive if their data queried by DeFi or other Dapps. Their information is protected with encryption and used in a secure runtime environment. 
2. Defi: Litentry user's ID and their assets prove is critical factor to determine their financial service. 
3. Dapps: Litentry user's cross chain information includes all activities in the whole cryptocurrency world. Litentry is the unique and unified entry point for their service.
4. Litentry node runner: Except get the block produce incentive, they can also run offchain worker for cross chain asset query service. They will be rewarded if the query result they submitted is correct.

### Scenario:

##### Defi: 

* Identity Registry: Litentry register and get Litentry ID with LIT token;

* Asset claim: If Litentry user also own assets in Bitcoin and Ethereum, they can link their account in Bitcoin and Ethereum at first. Then require Litentry to query their balance and create asset prove;

* Defi service: Litentry provide the SDK and API for Defi application, Defi can access Litentry ID and assets prove.Base on these information, Difi can put in into their algorithm model, then decide the loan amount, interests and credits score.

##### Cross Chain Identity:

* Identity Registry: Litentry register and get Litentry ID with LIT token;

* Dapp: Dapp service can get the aggregated cross chain account information via Litentry Id. Then Dapp can avoid implement every API for different blockchain network;

##### Smart contract with credit score algorithm:
* Identity Registry: Litentry register and get Litentry ID with LIT token;

* Smart contract: Litentry runtime provide raw data to smart contract deployed in Litentry network. Different smart contract can use diverse algorithm to compute the credits score. The applications can use one smart contract's data or use data source from different smart contracts to get their customer's financial profile.

## In the future
The Litentry runtime is under very active development now. More pallets will be implemented and integrated into Litentry runtiime. Litentry network will acquire the slot of both Kusama and Polkadot. Cross chain ID aggregation and query will be realized.
