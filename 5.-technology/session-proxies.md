# Session Proxies

Session proxies enable smooth UX even when Incognitee requires authentication for querying balances and messages.

For good security, we encourage users to protect their private keys in signer extensions for browsers or mobile wallets. 
These, however, come with a lot of user interaction if many actions require individual digital signatures.

Incognitee not only authenticates users when they want to perform state transitions (transactions, sending tokens or messages) 
but also when they query their balance or check incoming messages. This is necessary for privacy reasons.

To make the user experience smoother, we introduce the concept of session proxies.

## How it works

A session proxy is a keypair which is generated client-side and stored in Incognitee's sidechain state. Each session proxy has one of the following roles which defines what actions can be performed by the proxy on behalf of the owner without signer extension interaction:

* `ReadBalance`: Query the balance of the owner
* `ReadAny`: Query balance, messages and transaction history
* `NonTransfer`: Can send messages, but can't transfer tokens
* `Any`: Has full authority on behalf of the owner

These roles only apply to the Incognitee shard you register the session proxy on. They have no effect on other chains or shards.

As session proxies are stored on encrypted sidechain state, you can use them across devices and browsers. Just authenticate each new session with your owner account using the extension or mobile app and you can use the session proxy from then on.

## Why do I need to pay a deposit?

Your session proxy is stored on the Incognitee shard. Onchain storage is costly and we need to prevent state-bloat. Therefore, we ask for a tiny deposit for each session proxy you register (currently limited to one per owner account). Once you unregister the session proxy, the deposit is returned.




