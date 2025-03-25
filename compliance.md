---
description: Balancing Privacy and Compliance
---

# Compliance

Incognitee is committed to privacy-by-default while ensuring compliance with regulatory requirements. Striking this balance remains largely uncharted territory in Web3. Opinions on this matter are highly polarized: some projects refuse to engage in anti-money laundering (AML) efforts entirely, while others introduce explicit backdoors for authorities. Integritee rejects both extremes.

The key requirement for compliance is enabling law enforcement to access specific data when there is a reasonable and legitimate suspicion of serious crime. While this is necessary for compliance in many jurisdictions, it is not always sufficient. Instead of conforming to traditional national models, we propose a novel approach and argue why nation-states should accept it:

**Law enforcement must have necessary tools in a functioning society, but mass surveillance must be avoided.**

Since blockchains do not inherently fit within national jurisdiction models, we must design a solution from first principles.

***Disclaimer**: This document does not constitute legal advice. The compliance measures outlined here are based on our current understanding and may not ultimately meet all regulatory requirements. Individuals and businesses must conduct their own research to determine whether they can legally use Incognitee in their respective jurisdictions.*

## Incognitee Compliance Requirements

To establish compliance, we first outline the key stakeholders and their requirements:

### Individuals
- Expect privacy by default
- Oppose mass surveillance by both state and private actors
- Want the freedom to use Incognitee for legitimate purposes without legal risks
- Require a maximum retention period for sensitive data ("right to be forgotten")

### Validateer Operators
- Seek the ability to operate nodes for profit without legal risk

### Law Enforcement Detectives
To investigate crimes, law enforcement may need:
- The ability to trace funds from an input (shielding) event to their destination

### AML Compliance Departments
Banks and exchanges must verify asset origins. They may require proof of beneficial ownership to determine:
- The source of funds for an output (unshielding) event

### National Governments
Governments may enforce sanctions on nations, individuals, or entities:
- Preventing specific jurisdictions from:
    - Using the service
    - Sending tokens to sanctioned entities

### Secondary Requirements
- **Preventing account poisoning:** Attackers must not be able to taint accounts by sending illicit funds
- **Selective disclosure:** Voluntary disclosure by one account holder must not compromise others; read keys must only reveal information about the disclosing subject

## Assumptions
To transition from an abstract framework to a practical implementation, we assume:
- Each Incognitee shard operates under a single jurisdiction (e.g., Switzerland)
- All validateers (nodes) within a shard are physically located in the jurisdiction
- A designated court represents the jurisdiction on-chain, acting via a multisig account or DAO

Different jurisdictions may impose distinct compliance requirements.

## Suggested Solutions

### Beta Stage: Limiting Shielding Amounts
A simple but effective AML measure is capping the value of shielded transactions. Until more sophisticated compliance mechanisms are in place, this will serve as an initial deterrent.

- Small transaction limits discourage money launderers and sanctioned entities
- Even with sybil attacks, large amounts cannot achieve meaningful k-anonymity

### Beta Stage: KYB (Know Your Business)
To accommodate businesses requiring higher shielding limits, Integritee, as the operator of Incognitee in its beta stage, can provide whitelisting subject to KYB verification.

### Enforced Selective Disclosure and Freezing

#### Immutable Event Log with Per-Account Encryption

- Validateers log each financial transaction as encrypted ciphertext in a public and tamper-resistant event log (e.g. [EventStore](https://www.eventstore.com/))
- Each account has a unique symmetric log key stored securely within Incognitee
- Only account holders can decrypt their transaction history
- Courts, authorized by their jurisdiction and authorized on an Incognitee shard, may grant law enforcement access to an account’s log key when legally justified

#### Voluntary Disclosure (Proof-of-Innocence)

Users can provide proof-of-origin to AML compliance departments without revealing unnecessary details:
- By generating read-keys, users can trace funds back to shielding events
- Zero-knowledge proofs (ZKPs) ensure only relevant transaction links are disclosed, preserving privacy of behavioral details which are not relevant for AML

#### Handling Sanctions

Sanctions can be enforced through:
- **Blacklist mechanisms:** Validateers can block attempts to shield funds from sanctioned addresses
- **Account freezing:** Courts may be authorized to freeze Incognitee accounts

#### Mitigating Backdoor Risks

To prevent courts from abusing their authority (e.g., mass freezes or universal disclosure):
- Court actions are **rate-limited** (e.g., limited interventions per day)
- Court interventions are logged transparently and published by validateers

## Secure Event Logging and Data Retention

To prevent account poisoning and excessive data exposure:
- A **quarantine mechanism** ensures receivers actively accept incoming transactions
- Logs are encrypted per account and only accessible to the respective owner (unless legally disclosed by the court)
- Log retention is jurisdiction-dependent, after which:
    - Log-keys are rotated at fixed intervals
    - Deleting an encryption key equates to deleting the log content

<figure><img src=".gitbook/assets/ELIAS-eventlog.drawio.svg" alt=""><figcaption><p>Event Log with per-account encryption, enabling selective disclosure of transaction history</p></figcaption></figure>

## Cryptographic Considerations
To ensure security and efficiency:
- The symmetric encryption algorithm must be **quantum-safe** and **ZK-friendly**
- Potential candidates include:
    - [Poseidon](https://www.poseidon-hash.info/)
    - [Rescue Prime](https://eprint.iacr.org/2020/1143)
    - [MiMC](https://eprint.iacr.org/2016/492)

This approach balances privacy and compliance while maintaining decentralization and user control. By leveraging cryptographic techniques and trusted execution environments, Incognitee ensures lawful oversight without enabling mass surveillance.

