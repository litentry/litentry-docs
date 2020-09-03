# Token Economy

## Economy Participants

#### Identity Staker:
 The users who has an identity record on chain, and has stake the identity into identities pool.
#### Identity Validator: 
After the staking identity of identity staker is confirmed on chain, he will become identity validator for the next few blocks.
#### External Storage:
 An decentralized storage records all the related data of the identity (Currently IPFS, in the future we may add more database support)

#### Node:
 The maintainer of the network, it task is to record the state of the network, and respond to data matching queries, sending data access request to external storage, and use off-chain worker to validate the correctness of the identity staking data.
#### Data Buyer: 
An entity have either one of following two types of requirement is data buyer:
Arbitrary identity data: request a matching identity (list) according to the types/requirement data of certain identity: in this case, the buyer will need a authorization token from the identity.

#### Data Origin (Data Generator): 
there are three types of data origin:
1. Decentralized services / apps, it generate the data when user interact with dapp is signed by the data generator.
2. Traditional app / services, they may offer data migration services, it maybe signed or not. If it is signed, and data generator is register on the Litentry network, the data generator also benefits from data queries.
3. User generate the data by his own.


## Identity Staking Process

#### Identity Preparation: 
A identity staker who want to stake an identity into identities pool, need first has the required data type and format anchored to this identity, and the data is stored correctly in the External Storage. 

#### Identity Data Picking:
 Then the user chose which kind of the data he want to staked into the pool, only the picked type will be available for data matching, also the more data he chose, the more benefits he get, staker will need also pay a validation fee to the network and a basic staking deposit.

#### Staking Identity Validation:
 The data will be send to random selected identity Validator on chain, identity validator will try to prove if the data is correct. Here is three possibilities:
 * If any one of the validator reject the data, the staking process is failed, and part of thee fee will be returned, validator got no money.
 * If all validator proved the data, and identity with authorized types will goes into identities pool, fee paid to validator.
 * Same as above, If all validator proved the data, and identity with authorized types will goes into identities pool. But if in the next 30 block a malicious data is found for this identity, a part of reward of all the approved validator will be slashed, this slashing amount is decided by the existing blocks number (in this case, 30) of the existing malicious data.

#### Staking Identity Finalization:
The value of the identity data will be judged by its completeness and its relevance and according type and identity will be stored into on-chain storage. No identity data is stored, afterward each block the identity owner will receive rewards, and the reward is bound to the staking identity until it retire from the identities pool.

#### Staking Identity Retirement:
After certain block, the identity will be retired from the identities pool, after that, the rewards bound to the identity and the deposit will be release. User could update the identity data and then staking it again.

## Identity Query Process

According to the different data type required by data buyer. There are two types of query

### 1. Matching Query

#### Data Matching Request: 
Data buyer require a matching data with selected data type and criteria, which consist of a matching query.

#### Data Matching Pre-Making:
Node in the network will now start generate a list with random picking identities has the required type of data. The length of the list is decided by the fees the data buyer paid, the more data buyer pay, the bigger the list is. And the on-chain randomness make sure each time the result list would be different, so user has motivation to make the query two times.

#### Data Selection:
The list is send to the external Storage and the data is send back to the network and is received by the off-chain worker. Now the off-chain worker will use the selection algorithms to get the best suitable identity data for the buyer, and send the result back to user. The match winner will get the most of the fee paid by the buyer, others fee goes to the others in the list and data origin, also Litentry get small part of the fees.

### 2. Target Identity Query

#### Identity Data Request:
 Data buyer require a matching data with selected data type and identity id, the query also include an authorization token signed by the identity owner.

#### Request Validation:
 Node in the network will check the authorization token issuer, receiver, and validate block number. And finally decide if it is a valid request.

#### Request Finalization:
 A data request event is triggered, the off-chain work start to request the certain data from external storage, once it receive it, it will send a http request back to the data buyer. Fee is all paid to the identity owner and its related data origin, Litentry get a small portion.

## Incentivization

Basics:
LTT is the native token of Litentry Network, each block the network will give a fix amount reward to the identities owner of identities in identities pool.
In the staking finalization process, the value of the staking identity will be quantitated, so that the block stake reward will be shared according to identities staking value.

#### For Identity Staker: 
The profit of identity staker are from two parts, 
 1. Block Reward: Once staker data is into identities pool, Identity Staker will get the reward each block. 
 2. Matching Fee: Once the matching success with staked identity, the owner will get paid. 
So in the early stage, the matching request are not big enough, the identity staker will mostly benefits from block reward. When the network get more user and become mature, the share of matching fee will more evenly distributed to the quality identity staker. Thus a staker’s main benefit is matching fee.

#### For Identity Validator: 
They are motivated to become Identity Staker, so it is part of the responsibility to validate the correctness of the data.
If the origin of data is generated by the identity itself, then the validator will get reward once the data is used, since the validator has proved the authenticity of the data.

#### For Dapp as Data Origin:
Explicit benefits is the grants from Litentry Foundation, each success match will pay fee back to data origin. Implicit Benefits are: It is a new way to attract new users since users could harvest their own data. And for user from other DApp, there is no migration cost, they have motivate to make innovation instead building business protections.

#### For Node: 
As the network maintainer, they will get native token reward from the network.


#### For External Storage: 

User pays their own storage fee to the external storage, so they are willing to provide their services to our network.
