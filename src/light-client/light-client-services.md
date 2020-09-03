# Light Client Services

### Concept
Light Client should support all the networks on Substrate, and each of them have a node, so we should not pre-package all the nodes into the App, but support the app to download the most recent binary files and save them into the app. It should have at least “chose network”, “start service”, and “stop service” button. And most of the time it should be running in the background and work as an iinterface for all the apps to interact with a certain network.

In addition to giving apps a decentralized feature that talk to the network. An app could register an event subscribing on the light client service and push notifications to the user. So that the notification does not need to go through Android’s or Apple’s message center. A challenge would be how to always keep the light client app alive,  and when the user powered off the phone, the light client would stop receiving messages (a breakpoint resume function could be implemented for the user to get events from the last fetched block).

#### Android Implementation

The binary could successfully be compiled with the guide here and runned on Android Devices. 

To keep the light client always living in the background, we need to use Service, but the policy changed from time to time.

a minimal implementation: [https://github.com/hanwencheng/LightClientServices](https://github.com/hanwencheng/LightClientServices), which supports users to download the binary of Flaming Fir, and run the service in the background.
