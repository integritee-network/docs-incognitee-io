# Private Messaging

The Incognitee messenger has been designed with privacy by default. The unique features of this specialized messenger are:

* metadata-frugal: Thanks to its design, the amount of metadata which operators of validateers are able to collect is close to nothing. The operator does not learn *when* *who* *communicates* with *whom*. 
* blockchain-addressing: Write e2e encrypted messages to blockchain wallet addresses
* auto-delete: Messages are automatically deleted after a certain time
* decentralized: The messenger is a decentralized application (dApp) running on the Incognitee sidechain which is operated by an unpermissioned set of validateers (restrictions apply during beta phase)
* private token transfers: As part of the Incognitee sidechain, the messenger can transfer tokens along with private messages. 

## How it works

Incognitee sidechains host a ringbuffer of all messages up to a limited buffer size. The more messages are sent, the earlier the messages get purged from the buffer. This design allows us to solve multiple difficult challenges at once: 

* data availability: As the message buffer is part of the sidechain state it has to be replicated by every validateer who wants to produce blocks and earn rewards.
* strong privacy: The entire message buffer fits the confidential enclave memory. This allows querying messages to self or sending messages to others without leaving any traces beyond the TLS connection you establish into the enclave.

should the messanger enjoy wide adoption, retention time may become impractically short. In that case the message buffer can be used as a short-time cache and users can pay extra for off-shard encrypted retention. 

<figure><img src="../.gitbook/assets/incognitee-docs-messaging.drawio.svg" alt=""><figcaption></figcaption></figure>

## Comparison

The landscape of messengers is vast and diverse. In order to show where we place the Incognitee messenger, we provide a few comparative comments to popular messengers: 

* WhatsApp, Signal, Threema: centralized e2e encrypted messengers. They are metadata-rich as operators can collect when you communicate with whom, even if messages are (usually) e2e encrypted. With the exception of Threema you need a phone number to register.
* Telegram: Not private in any practical sense. Unencrypted by default. Centralized. Enables chat groups with large number of members
* [SimpleX](https://simplex.chat/): federated e2e encrypted messenger which generates minimal metadata. Very good choice for bilateral and small group chats. Doesn't support blockchain addressing or token transfers. 
* [Bitmessage](https://en.wikipedia.org/wiki/Bitmessage) The OG in blockchain messaging. Also works as a ringbuffer for encrypted messages, but the buffer is public and leaks pseudonyms. For query privacy, users need to download the entire bitmessage chain which is not necessary for Incognitee. 
