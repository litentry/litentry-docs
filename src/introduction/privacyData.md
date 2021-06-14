# Privacy data feeding and protection

The legacy verification process has many problems with regards to the privacy of data generation as an example

1. If a user come to Hotel with his digital key (claim). The smart lock itself could generate data, and each time the user entered the room, this data is generated, but they are harvested by the hotel, and never reach to user.

2. <match>The Data generated are combined with user's accountID (public address), when these authorizations (claims) be more enough, it will be practical for the external companies to monitor the on-chain state, and build user profile.</match>

To resolve this problem, and let the user get their data, we have designed our new method based on Substrate offline worker and crypto algorithms based on Schnorr25519.

1. To protect user's data, we migrate the data generation process on to Substrate, after the verification process, the crucial arguments like user address, verifier, time, token hash will be send into blockchain with a `verifier` extrinsic. Which is independent with off-line verification, thus it will not affect the verification time. Then the data will be generated in offchain worker, generate access token to user's storage, and then feed the data back to user.

2. To protect the user data, we will use HDKD feature to periodically generate new soft derivated key pairs for certain user. Verifier can prove that the address belongs to the parent keypairs using crypto algorithms. Thus user will not need to always show only the one public address. Another key point is to use ring signature, which will hide user's signature <match>behind bunch of people.</match>   Child address generation feature is already implemented in our crypto wallet and Ring signature is our current experiment direction.

The workflow of user data feed could be seen in the following diagram

![User Data Feed Diagram](./dataFeed.png)

Related Article about Off-Chain Worker: [https://www.parity.io/substrate-off-chain-workers-secure-and-efficient-computing-intensive-tasks/](https://www.parity.io/substrate-off-chain-workers-secure-and-efficient-computing-intensive-tasks/)
