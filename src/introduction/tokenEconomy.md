# Token Economy

## Economy Participants

#### Identity Staker:

 The users who has an identity recorded on chain, and has chosen to stake their identity and its related data into an identities mining pool.

#### Identity Validator:

 <mark>After the staking identity of identity staker is confirmed on chain, he will become identity validator for the next few blocks. *no idea what this means*</mark>

#### External Storage:

 A decentralized storage records all the related external data of the identity (Currently only IPFS, in the future we may add more database support)

#### Identity Staking Data

 The data that is staked in a mining pool for a particular identity that has chosen to stake their associated data.

#### Node:

 The node maintains the integrity of the network, the nodes task is firstly to record the state of the network <mark>*onchain?*</mark>, and secondly to respond to data matching queries by sending data access requests to the external storage and using off-chain workers to validate the validity of the identity staking data.

#### Data Buyer:

An entity has either one of the following two types of requirement is data buyer <mark>: Arbitrary identity data: request a matching identity (list) according to the types/requirement data of certain identity: in this case, the buyer will need an authorization token from the identity. *I cannot work out what two requirements that the data buyer has*</mark>

#### Data Origin (Data Generator):

there are three types of data origin:

1. Decentralized services/apps generate data when user interact with the dapp. This data is signed by the data generator.
2. Traditional services/apps may offer data migration services in this case the data may be signed or not. If it is signed and the data generator is registered on the Litentry network, the data generator also benefits <mark>(benefits how? financially?)</mark> from data queries.
3. User generate the data by his own.

## Identity Staking Process

#### Identity Preparation:

 An identity staker who wants to stake their identity into the identity staking pool first needs to have the required data type and format attached to this identity, and the data must be stored correctly in the External Storage.

#### Identity Data Picking:

 Then the user chose which kind of the data he want to staked into the pool, only the picked type will be available for data matching, also the more data he chose, the more benefits he get, staker will need also pay a validation fee to the network and a basic staking deposit.

#### Staking Identity Validation:

The data will be sent to random selected identity validator on chain. The selected identity validator will try to prove if the data is correct or not.
<mark>*I am guessing that the randomly selected validator can reject or accept the data before it is sent to the remaining validators?*</mark> There are three possibilities:

* If any one of the validators reject the data, the staking process fails, and part of the staking fee will be returned and the validator will not be paid.
* If all validators validate the data then identity with authorized data will be placed into the relevant identity pool, a validation fee is paid to validator.
* Same as above, if all validators validate the data then identity with authorized data will be placed into the relevant identity pool. But if in the next 30 block any malicious data is found for this identity, a part of reward of all the approving validators will be slashed, this slashing amount is decided by the existing blocks number (in this case, 30) of the existing malicious data.

#### Staking Identity Finalization:

The value of the identity data will be judged by its completeness and its relevance and according type and identity will be stored into on-chain storage. <mark>No identity data is stored, afterward each block *I cannot work out what this is saying*</mark> the identity owner will receive rewards, and the reward is bound to the staking identity until it retire from the identities pool. The value of the data being staked is quantified and the staker will earn staking rewards in proportion to the value of the data staked.

#### Staking Identity Retirement:

After certain block, the identity will be retired from the identities pool, after that, the rewards bound to the identity and the deposit will be released. User could choose to update the identity data and then restake it to earn further rewards.

## Identity Query Process

According to the different data type required by data buyer. There are two types of query

### 1. Matching Query

#### Data Matching Request:

 Data buyer submits a request for data with a selected data type and criteria thsi is called a matching query.

#### Data Matching Pre-Making:

 The Nodes in the network will now start to generate a list with randomly selected identities that have the required type of data. The length of the list is decided by the fees the data buyer selected to pay, the more data the buyer pays for, the bigger the list. The on-chain randomness makes sure that each time the result list will be different, <mark>thus incentivising the data buyer to make multiple queries.*I am not sure if my interpretation of this is correct*</mark>

#### Data Selection:

 The selected list of identities is sent to the external storage. The data is aggregaed and sent back to the network and received by an off-chain worker. The off-chain worker will use the selection algorithms to get the most suitable identity data for the buyer. This data is then sent back to the buyer. <mark> The match winner will get the most of the fee paid by the buyer, others fee goes to the others in the list and data origin *I got totally lost here not sure who the match winner is*</mark>. Litentry will earn a small part of the fees paid.

### 2. Target Identity Query

#### Identity Data Request:

 Data buyer submits a request for specific data associated with a specified identity (the data staked for a specific person). The query must include the matching data type required and the identity id of the relevant identity staker. For user security the query must include an authorization token signed by the identity owner.

#### Request Validation:

 <mark>A</mark>node in the network will check the authorization token issuer, receiver, and validate the block number. From this the node will validate the request.

#### Request Finalization:

 Once the node has validated the request a data request event is triggered, the off-chain worker starts to request the specified data from external storage, once the data is received, it is sent as an http request back to the data buyer. A fee is paid to the identity owner <mark>and its related data origin *I have no idea what the related data origin is*</mark>, Litentry will earn a small administration fee.

## Incentivization

 Basics: LIT is the native token of Litentry Network, each block the network will give a fixed block reward to all identity stakers in the identity staking pool. In the staking finalization process, the value of the staking identity data will have been quantified. The block reward will be distributed to identity stakers in accordance to this quantified identity staking value.

#### For Identity Staker:

 Identity stakers earn profits from two parts,

 1. Block Reward: Once staker data is accepted into the identity staking pool, the Identity Staker will get the reward for each block.
 2. Matching Fee: When the matching query with staked identity succeeds, the owner will get paid. In the early stages, where there are not many matching requests, the identity staker will mostly benefits from block reward. When the network gets more data buyers and becomes mature, the share of matching fee will more evenly distributed to the high quality identity staker. Thus in the long term an identity staker’s main benefit will be the matching fee thus incentivising an identity staker to stake the highest quality data possible.

#### For Identity Validator

 <mark>They are motivated to become Identity Staker, so it is part of the responsibility to validate the correctness of the data. If the origin of data is generated by the identity itself, then the validator will get reward once the data is used, since the validator has proved the authenticity of the data. *I almost get what is being said here but I think I still have a confusion between the identity validator and the identity staker. It almost feels like these are being considered to be one by Litentry but in my model I still see them as different.*</mark>

#### For Dapp as Data Origin

 <mark>Explicit benefits is the grants from Litentry Foundation, each success match will pay fee back to data origin. Implicit Benefits are: It is a new way to attract new users since users could harvest their own data. And for user from other DApp, there is no migration cost, they have motivate to make innovation instead building business protections. *I would need to understand this better*</mark>

#### For Node

 As the network maintainer, a node will get native token reward (LIT) from the Litentry network.

#### For External Storage

 The fee that the identity staker pays when they stake is used to pay storage fee to the external storage for their data. This matches the decentralised external storage business model perfectly and they are therfore willing to provide their services to Litentry network.
 