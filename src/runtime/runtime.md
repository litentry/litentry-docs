# Runtime

Github Repository: [https://github.com/litentry/litentry-node](https://github.com/litentry/litentry-node)

There are two pallets from litentry both account-linker and offchain-worker.
<!--- <mark>*Neither of these pallets exist on this path*</mark> The account-linker and offchain-worker are moved to the Litnetry pallets repo -->
[https://github.com/litentry/litentry-pallets/blob/dev/pallets/account-linker/src/lib.rs](https://github.com/litentry/litentry-pallets/blob/dev/pallets/account-linker/src/lib.rs)

[https://github.com/litentry/litentry-pallets/blob/dev/pallets/offchain-worker/src/lib.rs](https://github.com/litentry/litentry-pallets/blob/dev/pallets/offchain-worker/src/lib.rs)

### Abstract

The identity runtime protocol links all the cross chain accounts to make an unique Litentry Identity. After the accounts are linked, the Litentry user can trigger the asset claim via a transaction. The Litentry offchain worker will query your assets in the other blockchain network and generate asset proofs on-chain. Any Defi or other Dapp can then use this information for their service:

1. Account Linking: Litentry user signs the specific data with their private key.

2. Asset Claim: Litentry user asks Litentry runtime to query its assets and generate a proof.

3. Defi or other Dapp: Use the Litentry ID and its assets proof for their service.

### Stakeholders

1. Litentry user: Users register with the Litentry network, they can get the token incentive if their data is queried by a DeFi or other Dapps. Their information is protected with encryption and used in a secure runtime environment.
2. Defi: With Litentry identity, users can view their personal information, including credit and on-chain reputation. This information can be applied to mortgage rates and credit borrowing in DeFi lending.<!-- <mark>*I have no idea what this is saying*</mark> update the content-->
3. Dapps: Litentry user's cross chain information includes all activities in the whole cryptocurrency world. Litentry is the unique and unified entry point for their service.
4. Litentry node runner: They will earn the block production incentive and they can run offchain workers for cross chain asset query service. They will be rewarded if the query results they submit are correct.

### Scenario:

##### Defi:

Litentry can be used to provide a full credit history for a user. This credit history can be used in a Defi application or service for borrowing. By using credit histories, a full access to the users history and their assets a lending application can lend money with less collateral thus reducing the need for the current scenario where extremely overcollateralised loans are given. This would work as follows.

* Asset claim: If Litentry user also owns assets in Bitcoin and Ethereum, they can link their account from Bitcoin and Ethereum. Then they request Litentry to query their balance and create asset proofs;

* Defi service: Litentry provides the SDK and API for Defi application. The Defi service can access Litentries ID and asset proofs, based on this information, the service can use this data in their algorithmic model. Based on the above data they can decide on an appropriate loan amount, interest rate and credit score.

##### Cross Chain Identity:

Litentry data and account aggregation service can help Dapp developers to avoid having to implement API calls to numerous BlockChain networks.

##### Smart contract with credit score algorithm:

Lite entry supports smart contracts being built and deployed in the Litentry network. Different smart contracts can use different algorithms to compute the credit score. The Dapps being built for Defi can use one or more of these smart contracts to get their client's financial profile and credit rating.

## In the future

The Litentry runtime is under very active development now. More pallets will be implemented and integrated into Litentry runtiime. Litentry network will acquire the slot of both Kusama and Polkadot. Cross chain ID aggregation and query will be realized.
