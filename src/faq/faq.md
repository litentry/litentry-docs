# FAQ

>  What is the common use case of the identity protocol?


In our protocol, we basically analog most authorization scenarios into a common protocol with four elements: d1. Person or IoT devices Identity d2. Authorization d3. Member's who holds the Authorization d4. External data related to the Identity. Here the Authorization token is similar to the ERC721 standard but not the same, it could be used to help understand the idea. The common idea is that the authorization is a piece of data created by the d1. Person or IoT devices Identity and send to a d3. Member. The Specification of each d1. Person or IoT devices Identity will be saved as d4. External data. This ownership and specification could be proved by the whole network. 


Take door lock for example: An Airbnb host could use a smart lock to issue the digital key on our protocol, the user who has Parity-Signer Wallet (for example) could fetch the token data (d2. Authorization) and send it to the lock by a p2p way (Bluetooth for example) for validation. The lock will interpret the token data with its own pre-defined interpreter function (on-chain or off-chain, still need to think), like how many time a user may enter, what is the entry duration. By this way, the d1 Person or IoT devices could be shared in a decentralized and a securer way. We suppose such kind of authorization would fit the normal business (hotel) and sharing economy very well.


> Why use non-fungible-token as key rather than a signed message, e.g. a message signed using the digital key and can be validated by the lock off-chain.


Signing transaction way works in authorization and it is simple. The basic of token authorization model is to validate a piece of information which is sent by the owner. These pieces of messages could be encrypted in the transaction as a message memo, and even transfer to others with last message data include or using a UTXO model.


In comparison, The "non-fungible-token way" or "ERC721 Standard way" gives a state map of all the authorizations and identity of the IoT device or people. The advantages are:


1. The relationship between d1. Person or IoT devices Identity d2. Authorization d3. Member's who holds the Authorization could be checked easily, and this is very useful in many scenarios. For example, in an apartment sharing business, the user could know how many keys (tokens) are existed for a certain lock at the moment and further check the ownership of all other keys (tokens). 

2. Bulk transactions are more efficient and easy to update (even no need for loops). For example, an identity could easily recall all his authorized tokens, or updates existed tokens information.

3. A state explicitly shows the relationship and will be easy for understanding, and cross-chain programming. The further cross-chain function call will be based on the state information on different parachains.


In addition, the off-chain validation is still possible since the proof of token could directly be the identity (hash) of the token, and its information is retrievable from the state map. User with this information could send it to an off-line validator. ( Or a compromise way is that a validator regularly syncs with blockchain for the tokens and owners of identity, or totally an online validator).


> why do we need a GraphQl server? Is it worth the trade-off (complexity, centralization) as opposed to requests being validated directly on chain?


A GraphQl is basically an API server, we have two different views of its usage. 


1. In a short view, since currently there are not so many libraries like oo7 which can directly connect with Substrate Runtime and external IPFS storage. An API server will currently offer fast development and could be used as a good demo for application developers, it could be regarded as Infura on Ethereum.


2. In a long-run view, we supposed it could be a query server for historical and caching server, which could offer fast access for the historical data, good infographics from database, caching the data by event listeners and queries, and reduce the load of the blockchain. Though it is with tradeoffs and comprises to the decentralized architecture, the most important validation and issuing functions will still be accessible directly by Blockchain.


So in summary, the GraphQl API server is a necessary-to-have thing, but whether to use it will be mostly chosen by the application developer. 


> What is the difference between ID Chain and Lock Chain and the need for each?

Litentry is aimed to offer a basic protocol and related framework, which could be used for fast application development. Both the ID chain and Lock chain are one application based on it. 

The traits of these two chains are in the same protocol with slight differences. Take ID chain, for example, The registry could be the citizen offices in a different city. Permissions would be that the different Right bind with certain people, like (boolean value for over 18 age, int value for tax level, etc). Permissions could be assigned to only one Member, but a member could have more than one Permissions.


The same in lock chain is that the Locks are a list with all different kinds of lock, the lock owner who has the private key of the lock may issue the access right token to the member, like multiple entry token, or a one-day-pass token. A member could have a different token with different locks, but one token could be only assigned to one person.


Though there are similarity and difference based on the implementation of the protocol of different traits of parachain. The main difference between these parachains is that they have different cross-chain function based on that. The cross-chain function could be e.g. A insurance (which authorized insurance token) calculate the healthy insurance working permit of ID Chain; the Lock chain will issue the entry token of a shisha bar with validating the age on ID chain; A gym will offer a special membership token to the people who have the entry token of co-working space, etc. All these cross-chain issue and validation will be defined by the cross-chain function on different para chains with the same protocol.


In addition to that, separate these chains will gain the flexibility to different business scenarios by adding the parachain-scope function. For example, an IoT device Chain with temperature monitors of different locations. A value of all the registered temperature monitors on 24:00 every day could be harvest directly to external storage. But if a user wants to get a piece of detail information on a certain time, he needs to has an authorization token for querying that data. 
