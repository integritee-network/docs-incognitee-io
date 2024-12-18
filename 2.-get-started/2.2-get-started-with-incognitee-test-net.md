# 2.2 Get started with Incognitee Test Net

## Incognite Paseo Test Wallet  <a href="#incognitee-cli-tutorial" id="incognitee-cli-tutorial"></a>

You can already test a simple version of the Incognitee Wallet on Paseo. \
\
Follow the link : [https://try.incognitee.io](https://try.incognitee.io)

Once you enter the website, you will see the Incognitee wallet, which is already generating new wallet for you.&#x20;

1. The first step is to obtain free PAS tokens on Paseo via the button below in the window. There you should copy the address into your clipboard and go to the Paseo faucet. \
   \


<figure><img src="../.gitbook/assets/image (20).png" alt="" width="563"><figcaption></figcaption></figure>

2. Enter your copied wallet address in the faucet to get your first 100 free PAS. After this, you can close this window and return to the Incognitee web wallet.&#x20;

<figure><img src="../.gitbook/assets/image (21).png" alt="" width="563"><figcaption></figcaption></figure>



3. You can now also close the pop-up screen and continue interacting with the wallet. Now you can also see on the top, that you are currently active on the only available test network Paseo with one available Token PAS.  \
   In the center of the screen, you can see your current public balance,  as you just retrieved 100 PAS from the faucet.  From here you can now either shield your balances to the private L2 or switch to your private balance.&#x20;

<figure><img src="../.gitbook/assets/image (22).png" alt="" width="563"><figcaption></figcaption></figure>



4. By selecting "Shield" you can now transfer your PAS to the private L2 layer.&#x20;

<figure><img src="../.gitbook/assets/image (17).png" alt="" width="563"><figcaption></figcaption></figure>



5. Switching now to the private balance, you can either send or receive PAs tokens privately and instantly without leaving any trace on chain. Or you can unshield the PAS tokens back to layer 1.&#x20;



<figure><img src="../.gitbook/assets/image (18).png" alt="" width="563"><figcaption></figcaption></figure>



## Under the hood

#### Check sidechain activity

Visit the [Integritee Network on Paseo explorer](https://polkadot.js.org/apps/?rpc=wss%3A%2F%2Fpaseo.api.integritee.network#/explorer) where you can see events whenever sidechain blocks get finalized:\


<figure><img src="https://hackmd.io/_uploads/rJsCT-uFT.png" alt=""><figcaption></figcaption></figure>

As privacy is our main feature, you can’t see much more here. The `BlockHeaderHash` helps you proving that you sent funds to someone. By default, recipients just observe a change in their balance but they have no clue where the funds come from unless you tell them and provide a merkle proof for the sidechain block inclusion of your transfer.

However, as shielding and unshielding events are publicly happening on Paseo, you can observe shielding/unshielding activity on the vault account on [subscan](https://paseo.subscan.io/account/5CBWPstfcW7dPYGdUG4kVDZSQq9Q9Ed65LT2Eu1inhJRoY8e?tab=transfer).

The balance of the vault account will always exactly match the total supply on the respective sidechain shard.

#### What are shards and mrenclaves?

Each instance of an Incognitee sidechain is identified by a _shard identifier_ and we’ll need to tell the validators which shard we’d like to talk to. Think of it like the genesis hash of a L1 blockchain.

The `MRENCLAVE` identifies the validator code which is executed in Intel SGX enclave (it’s basically the hash of the enclave binary). Your call will only execute if the validator runs the code you expect it to run.

#### Why should I trust validators?

Because they can’t cheat and they can’t see your data. That’s what TEEs guarantee. But how should you know that the validators actually run the correct code in a TEE? You can authenticate validators thanks to Integritee’s remote attestation registry at [enclaves.integritee.network](https://enclaves.integritee.network/?rpc=wss%3A%2F%2Fpaseo.api.integritee.network).

There you can find the validator for this tutorial if you search for the url you’re using `wss://integritee-1.cluster.securitee.tech:2000` and it will tell you the verified MRENCLAVE which has been remotely attested using [our decentralized DCAP process](https://docs.integritee.network/4-development/4.5-attesteer).

