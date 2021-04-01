# Protocol

### Concept of Decentralization

The decentralization of Litentry includes following aspects:

* `Decentralization of identity storage`: User data, including identity credential, should be storage in the user's owned devices, instead of the central data server of a service provider.

* `Dentralization of idenity authentication`: The identity validator is connected to the decentralized network, and it validates the authentication request independently.

* `Decentralization of identity ownership`: The relationship of data, person, and identity is validated with a cryptographic calculation, and it is also record in the decentralized network instead of centralized service like Certificate Authority using in HTTPS.

* `Decentralization of Identity Data Allocating`: The user data generated when using third party applications/services is processed by the resolver function on the Litentry Network, <mark>this provider uses trustworthy data.*I am not sure what this is trying to say*</mark> , wich allocates data from multiple applications/services, as such users are able to create valuable user profile like health info, shopping history, etc.

### Definitions

* `User`: The originator of the data, the person who owns one or more identities or IoT devices.
* `Identity`: It is a generalized concept of identity, not only include the identity of person, but also any thing could generate claims like an IoT devices. A person could own multiple identities, like an identity in Germany, an identity as E-Resident in Estonia, or an identity as an game player.
* `Authorization`: <mark>The permission in the reality or</mark> the claim in the blockchain world. It is a piece of data a token that could proves a users ownership to a capability or a real world thing. Authorization could be the permission to read the age data of a person, or the ownership of a 3D printer on a certain day.
* `External Data`: It is the data generated when using an applications/services, like the shopping history when a user shopping in e-store, or the age data read from the aforementioned age proving request.

### Network Interoperability

Based on Substrate Network, Litentry aims to become a fundamental part in the Web3 infrastructure.

// TODO

* `Network Layer`: Polkadot is here to connect different blockchains
* `Runtime Layer`: The Litentry Pallet could be used for other Substrate network builders.
* `Application Layer`: Small business could build smart contract on Litentry network.
