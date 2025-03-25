---
description: Balancing Privacy and Compliance
---

# Compliance

Incognitee aims for privacy-by-default but also compliance at the same time. Balancing the two is mostly terra incognita in web3. The common opinion seems to be very polarized and other projects either refuse to help fight money laundering and other criminal activity entirely or - on the other end of the spectrum - deliver a plain backdoor to authorities. Integritee refuses to do either.

We see the main requirement for compliance to be the possibility for law enforcement agencies to gain insight into specific data subject to reasonable and legitimate suspicion of serious crime. Today, this may be a necessary - but not sufficient requirement to be considered compliant with many jurisdictions. But let’s look at the heart of the matter and think about a design from scratch:

**Law enforcement shall be enabled in any reasonable society - but wide-ranging surveillance shall not.**

Blockchains don’t fit into any national jurisdiction model, so we should come up with something ourselves and argue, why nation-states should accept it.

This is what we’ll attempt to do in the following.

## Incognitee Compliance Requirements

Let’s first describe the main stakeholders and their requirements.

### Individuals
* desire privacy by default
* reject mass surveillance both by state actors or private companies
* desire the freedom to use Incognitee for legitimate reasons without risking legal jeopardy
* right to be forgotten: maximum retention time of sensitive data to be enforced

### Validateer Operators

* desire the freedom to operate nodes without risking legal jeopardy

### Law Enforcement Detectives

To prosecute crime, detectives may need insights of the following kind in the context of Incognitee:

* given an input (shielding) event, where did the money go?

### AML Compliance Departments

Banks and exchanges are obliged to perform due diligence on the origin of assets they receive. In the context of Incognitee, they might need proof of the beneficial owner to know:

* given an output (unshielding) event, where did the money originate from?

### National Governments

May enforce sanctions on other nations, their citizens or selected individuals.

* prevent actors from specified jurisdiction to
   * use the service
   * send tokens to actors residing in sanctioned jurisdictions

### Secondary Requirements

* preventing account poisoning: an attacker should be unable to poison other accounts by simply sending black money to them
* voluntary disclosure by one account holder should not expose others: read keys should only disclose information about the disclosing subject

## Assumptions 

The following simplifications will be assumed to get from the very abstract to the practically feasible.

* Each Incognitee shard has a single associated jurisdiction, e.g. Switzerland
* all validateers (nodes) for that shard are operated within the geographical bounds of that jurisdiction
* jurisdiction names a court to be represented on-chain e.g. as a multisig account or some form of DAO.

Different jurisdictions may have different compliance requirements.

## Suggested Solutions

### Beta Stage: Limiting Shielding Amounts

One simple yet effective countermeasure to money laundering is to only allow relatively small amounts of value to be shielded. Before Incognitee has other measures in place, this is what we’ll do.

Small amounts are unattractive for both money launderers and sanctioned people and entities. Even if they find a way to sybil-attack and bypass the shielding limits, the k-anonymity they can obtain is very limited for large amounts.

### Beta Stage: KYB

To make Incognitee useful for businesses requiring larger shielding limits, Integritee as the operator of Incognitee during beta stage can offer whitelisting subject to KYB.

### Enforced Selective Disclosure and Freezing

Validateers send each financial transfer event to an immutable log (i.e. EventStore) as ciphertext, encrypted with a per-account symmetric log-key. The log-keys are only stored in Incognitee’s encrypted state and can only be read by the account holder. However, the court is authorized to disclose an account’s log-key to law enforcement of its jurisdiction, enabling its agents to read the account’s transaction history.

**Voluntary disclosure** (a.k.a. proof-of-innocence) is possible through read-keys (using the session-proxies feature): Let’s assume an individual wants to convince some banks' AML compliance department that their deposit originates from an account they control which in the past shielded funds to Incognitee - or, less invasive: proof that the funds don’t originate from an account which has been blacklisted a-posteriori. The disclosing individual would create read-keys for the AML department to follow the money back to the shielding event using the log-keys. Because such a trace leaks more information than necessary, the individual could generate a ZK proof over selected log entries which only prove the connection between input and output and hide detailed behavioral information.

**Sanctions** could be addressed in multiple ways: validateer operators can **blacklist** L1 addresses and block attempts to shield funds. But that will only work before the sanctioned entity has shielded funds. Another measure would be to authorize the court to freeze accounts on Incognitee.

With such far-reaching authorization, the court could potentially render Incognitee useless because it may freeze all its accounts or disclose information on all accounts. In fact, the court might effectively become a backdoor, which we strictly aim to avoid. Therefore, we suggest **rate limiting** and transparency of court actions. Pure cryptography can’t do that, but a network of trusted execution environments such as Incognitee can. Incognitee can restrict court interventions to N per day. Moreover, a transparent log of court interventions can be published by the validateer operators.

The diagram below shows what the event log could look like. For financial transactions from one account to another, we’ll introduce a quarantine account. The receiver will need to actively accept incoming transfers. This prevents account poisoning but also ensures that voluntary disclosure by one side doesn’t reveal information about the other side. Each account will store a symmetric encryption key on Incognitee state. Every transaction will then be logged in encrypted form and only the account holder can decrypt log entries affecting them (except for the court as described above). After the retention period required for the given jurisdiction, log entries should be purged. For this purging of logs to be meaningful, log-keys should be rotated in fixed intervals (deleting the encryption key is considered equivalent to deletion of the encrypted content).

<figure><img src=".gitbook/assets/ELIAS-eventlog.drawio.svg" alt=""><figcaption><p>Event Log with per-account encryption, enabling selective disclosure of transaction history</p></figcaption></figure>

The symmetric encryption algorithm for the log shall be chosen to be quantum-safe, yet ZK-friendly to allow lightweight proof-of-innocence. From what we know today, possible candidates could be: [Poseidon](https://www.poseidon-hash.info/), [Rescue Prime](https://eprint.iacr.org/2020/1143), [MiMC](https://eprint.iacr.org/2016/492)
