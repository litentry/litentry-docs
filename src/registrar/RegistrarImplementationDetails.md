

# Implementation Details

Github Repository: [https://github.com/litentry/litentry-registrar](https://github.com/litentry/litentry-registrar)



In this document, we introduce the Judgement level and implementation details of the Litentry registrar. At this stage, the Litentry registrar takes four confidence levels as judgment levels. Furthermore, We’d like to support `KnownGood` with well-known KYC organizations in the future. In the implementation details section, the Litentry Registrar Architecture is presented that includes Validators, Event Listener, ProvideJudgement Service, and Database Service. We also introduce a secure method using JWT to construct the verification protocol.

## Judgement Levels & Criteria

Officially, registrars on Kusama can provide the six levels of confidence for users’ identity:

* `Unknown`: The default value, no judgement made yet.
* `Reasonable`: The data appears reasonable, but no in-depth checks (e.g. formal KYC process) were performed.
* `KnownGood`: The registrar has certified that the information is correct.
* `OutOfDate`: The information used to be good, but is now out of date.
* `LowQuality`: The information is low quality or imprecise, but can be fixed with an update.
* `Erroneous`: The information is erroneous and may indicate malicious intent.
+ `FeePaid`: The judgement is requested by a user and the information is verifying in progress. 

Litentry registrar takes Unknown, Reasonable, OutOfDate, Erroneous as confidence levels, and clarifies criteria for  those judgement levels. 

If a user’s `display name`, `email`, `twitter`, or `element(previously called riot)` is verified, Litentry registrar comfirms the user's identity as Reasonable. Furthermore, Litentry registrar will also keep track of users' identity to see whether it’s out of date or not regularly. If a user doesn’t verify his identity timely,  his identity will degrade to OutOfDate. If a user intends to attack litentry registrar, e.g. DDOS, Litentry registrar will provide judgement with Erroneous and refuses to provide a judgment for him in a specific period.

As for LowQuality, it makes no sense to provide such a judgment for a requested user as a final judgement. Litentry registrar will automatically provide further hints to guide the user to update his identity. After all the information is verified correctly, the user will receive Reasonable. In this way, a user can not only save his fee (since we only provide one judgement for him) but also save his time (since Litentry registrar will point out imprecise or low quality identity timely).

At the current phase, Litentry registrar doesn’t support providing a judgement level of KnownGood since it needs cooperation with third-party KYC services. We’d like to support it with well-known KYC organizations in the future.

## Implementation Details
The key components of the Litentry registrar are shown as follows. It mainly includes Validators, Event Listener, ProvideJudgement Service and Database Service. Figure1.1 presents the architecture of the Litentry registrar, and Figure1.2 shows the main workflow of the registrar.

<p align="center"><img src="./registrar12.png" alt="litentryReggistrar" width="60%"/></p>

<p align="center">Figure 1.1 The Architecture of the Litentry Registrar</p>


The Event Listener listens to all events coming from the Kusama chain. Once a JudgementRequested event is triggered on Kusama and the JudgementRequested indicates to use the Litentry registrar, the Event Listener service will invoke Validators starting the verification process. 

At the current stage, the Validators consist of three verification services, Email, Element, and Twitter verification. After receiving the verification request from the Event Listener, the Validator will invoke those verification jobs. They will send a verification link to the users provided accounts and wait for user confirmation from their accounts. As soon as the user confirms all verification links, the ProvideJudgement service will complete the final step, providing judgement for the user. The implementation details will be introduced in the next section separately.

Once the user proves the ownership of the Email, Element, and Twitter account, the ProvedeJudgement service will send a JudgementGiven transaction on the Kusama to confirm the ownership of the accounts that the user provides.

The Database service will temporarily store users’ data, e.g. Kusama account, email, Element, and Twitter account, so that we can recover services from an unpredictable crash. After completing the verification service, those data will be removed from the server permanently.

<p align="center">
<img src="./registrar13.png" alt="litentryReggistrar" width="55%" height="60%"/></p>
<p align="center">Figure 1.2  The main Workflow of Verification process
</p>


### Security and Availability
We use JSON Web Token (JWT) to construct the verification protocol. A nonce and an ObjectID (comes from mongodb) are used to generate the JWT token to ensure security of the Litentry registrar. In this implementation, only the user who requests identity judgement, which implies his/her ownership of this Kusama account, will receive this encrypted token. Malicious users cannot construct this token because of an unknown encryption secret, since nonce and ObjectID  are encrypted. And the malicious user has no way to re-play the attacks. 

On the other hand, the websocket (TCP connection) can be easily reset by the remote peer due to long-time idle. In this situation, the events from the Kusama would be never captured since the disconnection between them. To prevent this situation, we capture the events from the underlying websocket connection and reconnect to the Kusama automatically whenever it’s reset by the peer.



### Reference
1. https://wiki.polkadot.network/docs/en/learn-identity#kusama-registrars











