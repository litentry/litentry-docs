# SubAuth

Check Web Demo [here](https://demo.litentry.com/)

Repository: [https://github.com/litentry/LitentryWebDemo](https://github.com/litentry/LitentryWebDemo)

On how to play with the web demo please refer to [this article](https://www.litentry.com/post/use-the-playground-apps-to-interact-with-litentry).

SubAuth is a protocol for web app applications to achieve a Substrate based authentication.

### The Object

* It should allow users to use his/her owned Substrate address to login to a third party website (that supports this login method).
* It should be easy to use and reasonably easy to setup.
* It should not compromise the security of the user's Substrate account.
* It should allow users to recover their credentials in case of loss or theft.
* It should not require knowledge of Cryptography or Blockchain with authentication.
* It should have reasonable latency for a login system.
* It should not cost users gas (or money) to login.
* It should be reasonably easy for developers to implement in their apps.

### The Implementation

1. User on a third party website and click login with Litentry Button
2. A preset account will come if user has logged before in the computer, or a QR scanner comes out for user to scan his/her Substrate account QR code.
3. At this time the third party website send a transaction to Litentry network with a challenge string and its receiver server address. And sign a JWT with challenge and server address embedded in it.
4. User now has to open the mobile app (best integrated with Substrate light client), it has watched the event of the auth request, and then sign the JWT with its private key and then send the signed double signed JWT to the server address.
 5. The server proved the token received by the user and then finish the logging process.
 6. After the usage of the third party web application or service, third party allocated the user browsing data/history and query the user's data resolver address, then user data is send back to the resolver and being process and harvested into user's own database.
