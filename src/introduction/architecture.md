# Architecture


### The protocol is mainly constructed with following parts:

* [Litentry Runtime](../runtime/runtime.md)
* [Litentry Authenticator Mobile App](../mobile-app/mobile-app.md)
* [Litentry DApp Playground](../web-app/web-app.md)
* [Litenry IPFS Data Center](../)
* [Litentry SDK](../sdk/sdk.md)
* [Litentry GraphQL Caching Server](../api/api.md)

![API Design](./design.png)

Other than web 2.0 architectures, we are suppose to build a decentralized ecosystem with Blockchain as backend services than cloud or single node server.

### Runtime

Litentry Runtime is built with Substrate, it inherits great features and best technologies in the industry. 

We use offchain worker to generate identity related data, and thus remove the uncertain and privacy issue by the client side applications.

We aim to be the Parachain of Polkadot Network. We will also benefit from the thriving cross-chain ecosystem.

### User Side

User has full control of identity data, data generated from Apps flows to user's decentralized storage like IPFS or Arweave. User's identities are anonymous, cryptographic separated.

#### Litentry Authenticator

On user side we have Litentry Authenticator as user's mobile data hub.

Personal users would like to use an application to manage all its identities, it could also become a Hub connected to different interest IoT devices. For example, directly buying the authorization or the data from other IoT devices. With the advantage of GPS of mobile phone, it could further integrate with LBS (Location Based Services).

In order to work in a fully decentralized scenario, itself also need to integrate a cold wallet, where could keep a user's private key in a secure environment provided by Android or iOS.

#### DApps build with Litentry Protocol

With Litentry SDK, developers could easily build fully decentralized Apps or Services. User could directly signin without password, without registration. Simply with Cryptographic QR code. App could use IPFS, Arweave or even on-chain key value database for storing user data, instead of storing data on backend server.

By this we are convert to an app-centric internet to a user-centric one.  

#### Litentry IPFS Data Center

Litentry uses OrbitDB to offer an IPFS database support. In Data Center, user may check their identity related data and tokens.

In the future we will implement Arweave and on-Chain key value storage.

### Middleware Layer

It mainly includes:

* Event listener and off-chain caching server:  With cached data it reduces the query load on the blockchain, furthermore, it saves the caching data on the centralized database in order to improve the speed of application-based blockchain query, like Infura for Ethereum. A relay script server is also built here, to automatically trigger an event on periodically regarding block generation.

* GraphQL caching server: Since IPFS is still under testing, we currently use graphql caching server to improve user experience for sync the data, it also caching anonymous data, and improve data query speed.

* Validation and query server: validate the authorization tokens with HTTPS request for IoT devices or application.

* Client side SDK library: The javascript binding library will directly connect the front-end applications with Blockchain, for example, React or React Native applications.
