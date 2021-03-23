

# Litentry Registrar

Github Repository: [https://github.com/litentry/litentry-registrar](https://github.com/litentry/litentry-registrar)

Litentry Registrar Support:  [Element Room](https://app.element.io/#/room/#litentry-registrar-support:matrix.org) or [registrar-support@litentry.com](mailto:registrar-support@litentry.com)

Litentry Registrar index on Kusama is 4, and the service fee is 0.04KSM.

**In the Twitter verification process, users need to follow the Litentry official registrar account, namely Litentry Registrar (@LitentryReg).**

## Introduction 
The user's account (public key, wallet address) on the blockchain can remain anonymous since it is loosely connected with the user's identity. However, a user with high reputation can be trusted by the community in the Polkadot ecosystem when he plans to be a validator or a councilor. In this document, we want to introduce a registrar service that focuses on automatic verifications, leveraging well-designed cryptographical challenges to further reduce human interventions. At the moment, Litentry registrar focuses on providing judgment with confidence for a user's `display name`, `email`, `twitter`, or `element name (previously called riot)`.  


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




## User Interaction 

In this section, we will introduce the user's identity verification process step by step. Firstly, users need to set their identity information on the chain. Then, they can request a registrar to provide identity judgment. Users declare a maximum fee and the registrar they are willing to pay and verify for the judgment. After that, the dedicated registrar can ascertain.

### Setting an On-chain Identity
Go to the Accounts page in Polkadot-JS Apps. The easiest way to add the built-in fields is to click the vertical three dots next to one's account and select "Set on-chain identity".

<p align="center">
<img src="./registrar1.png" alt="litentryReggistrar" width="75%" /></p>
<p align="center">Figure 1.3  Set Onchain Identity
</p>

A popup will appear, offering the default fields.
Currently, Litentry registrar only supports the following fields:

* `display name`
* `email`
* `twitter`
* `element (formerly known as riot)`

<p align="center">
<img src="./registrar2.png" alt="litentryReggistrar" width="60%" /></p>
<p align="center">Figure 1.3  Set Identity
</p>

Once users have filled in the information, they would like to store on-chain, click `Set Identity` to
submit the transaction.

Now Users have set the identity information on-chain, but that is not verified yet, so they should see a little gray icon beside users name. 
<p align="center">
<img src="./registrar3.png" alt="litentryReggistrar" width="40%" height="40%"/></p>
<p align="center">Figure 1.4 Account Example</p>


It is the time to interact with the Litentry's verification bot by submitting the judgment request to the Litentry Registrar.

### Judgement Request
Go to Developer->Extrinsic and select your account to submit the identity -> requestJudgement(reg_index, max_fee) transaction. This will request the registrar to validate the information you set on-chain earlier. The reg_index is the index of the registrar. For Litentry, use 4. The max_fee is the amount KSM to pay the registrar. Litentry Registrar service fee is 0.04 KSM.

<p align="center">
<img src="./registrar5.png" alt="litentryReggistrar" width="75%" /></p>
<p align="center">Figure 1.6 Judgement request</p>


</center>

### Verification Services
Since we provide the Email, Element and Twitter verification in our registrar at this moment, you will receive verification requests from those platforms. 

#### Email Verification
Users will receive an email called "Litentry Verification Service". Figure 1.7 is an example of email verification. Users only need to click the button "Verify Email Now" to complete proof of email address. Then they will receive another confirmation email that shows the email has been verified successfully.

<p align="center">
<img src="./email.png" alt="litentryReggistrar" width="50%"/></p>

<p align="center">Figure 1.7 Email Verification Example
</p>


#### Element Verification

As for Element, an invitation will be sent from the bot named "litentry-bot". Once the user accepts the invitation, "litentry-bot" will send a verification link. Users only need to click the link to complete verification of the element account. When it proves the user is the account owner, they will receive a confirmation message such as "Verified successfully" (see the figure below).



<p align="center">
<img src="./riot.png" alt="litentryReggistrar" width="50%"/></p>
<p align="center">Figure 1.8 Element Verification Example
</p>


#### Twitter Verification
In the Twitter verification process, users need to follow the Litentry official registrar account, namely Litentry Registrar (@LitentryReg). Users could also set their accounts to receive any private conversation in their privacy settings. Otherwise, they cannot receive the message from the Litentry registrar. 
Litentry Registrar will send a direct message associated with a verification link to the user. Once the verification link is clicked, 
the verification of Twitter is completed, and you should receive a successful verification message. The following figure is an example of the Twitter account verification process.

<p align="center">
<img src="./twitter.png" alt="litentryReggistrar" width="50%"/></p>
<p align="center">Figure 1.9 Twitter Verification Example
</p>


If everything has been verified successfully, you would see your account verification status has been marked as "reasonable" with a green tick icon on the account. And congratulations! Your identity should now show as a green "verified" checkmark on Polkadot-JS Apps.

## Registrar Fee
It is important to notice that no KSM are sent to the registrar at any time. You should NOT send or transfer funds. When calling the requestJudgement, the registrar fee will be locked and put aside. It will be transferred to the registrar only after the registrar finishes the judgment job. After all, we are using a trustless system. The judgement fee of Litentry Registrar is 0.04KSM.

### Reference
1. https://wiki.polkadot.network/docs/en/learn-identity#kusama-registrars
2. https://www.chevdor.com/post/2020/01/17/registrar1/











