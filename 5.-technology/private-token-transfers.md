# Private Token Transfers

Incognitee enhances your privacy while dealing with digital assets.
          But what does privacy mean and how does incognitee improve privacy?

First, let's explore why digital assets are generally
          **not** private. When dealing with crypto assets, your account is a
          pseudonym on a public ledger, much like a bank account number. Every
          single transaction this account does will be stored publicly forever
          and you have no right for deletion of the trace you left. If, at a
          certain point in time your pseudonym can be linked to your identity -
          i.e. because you send tokens to someone else - your entire behavioral
          history is revealed as is your balance.

Incognitee is a privacy-enhancing technology that allows you to shield your
          assets and transfer them privately. This means that you can send
          tokens to someone else without revealing your balance or transaction
          history. The recipient will not be able to see your balance or
          transaction history either. This is achieved by using a technology
          called
          [trusted execution environments (TEE)](https://docs.integritee.network/2-integritee-network/2.7-privacy-technology-trusted-execution-environments)
          . The TEEs we use are a hardware feature of server CPU's called
          *Intel SGX*. In addition, the
          [Integritee Network](https://docs.integritee.network/2-integritee-network)
          , a Polkadot parachain, performs independent, decentralized remote
          attestation of TEEs. Moreover, it gives finality to Incognitee
          sidechain blocks.

Incognitee is a layer 2 solution, maintaining a private ledger secured
          by TEE. All your transactions are confidential, only known to and the
          person your transacting with. Sender, recipient and amount are
          invisible to the public and even to the operators of Incognitee
          infrastructure.

For maximal privacy, we suggest to shield your assets to incognitee
          and from then on transact them on incognitee only. If you need to
          unshield back to L1, you can still benefit from k-anonymity: the
          public just sees that someone out of *k* individuals is the
          originator of an unshielding event. If *k* is large enough, you
          can plausibly deny it was you. You can influence the size of
          *k* by choosing popular amounts and timing.
