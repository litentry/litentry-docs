# Runtime

Github Repository: [https://github.com/litentry/litentry-runtime](https://github.com/litentry/litentry-runtime)

As Pallet: [https://github.com/litentry/substrate/blob/master/bin/litentry/pallets/template/src/lib.rs](https://github.com/litentry/substrate/blob/master/bin/litentry/pallets/template/src/lib.rs)

### Abstract

The identity runtime protocol abstract all the persons and devices authorization scenario, includes three basic definitions:

1. Identity Registry: a pre-defined key pair to present a person or a device.

2. Token: a non-fungible token issued by the identity.

3. Data: the related identity data, like identity meta information and token specification. 

![Identity Runtime Protocol](./runtime.png)

### Examples:

##### Person ID chain: 

* Identity Registry: crypto key pairs bind to national identity number;

* Token: a token created by the person, which could be used to validate the age;

* Data: the data of the person, e.g. birth date and place, gender, etc.

##### Lock Chain:

* Locks Registry: crypto key pairs bind to the smart IoT lock;

* Token:  a token created by the lock, which could be used as an entry key.

* Data: the definition of the token, e.g how many times could one token be used.

### Features

##### Cross Chain Validation

Such a protocol could be easily combined for the Polkadot cross chain feature, thus could realize many new ideas:

For example, the entry token on the lock chain need to be combined together with the personal ID chain, the entry token is only valid if the user's age is more than 18. The other personal data will not be exposed at the same time.

##### Runtime Specific Data Operation:

An IoT device manufacturer could have its own data operation functions, for example, it may harvest the data from all the temperature sensors and pay DOT to the sensor owners. 

##### Data Linking

The large data bind to the identity owner, i.e. person or devices, will be saved into an IPFS data server, the entry hash link will bind to their identity. The benefit of it is once the data updates, the old link will be also disabled. In order to always get the available data, others need to ask permission from the user. 
