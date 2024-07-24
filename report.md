# **Safe Audit Competition on Hats.finance** 


## Introduction to Hats.finance


Hats.finance builds autonomous security infrastructure for integration with major DeFi protocols to secure users' assets. 
It aims to be the decentralized choice for Web3 security, offering proactive security mechanisms like decentralized audit competitions and bug bounties. 
The protocol facilitates audit competitions to quickly secure smart contracts by having auditors compete, thereby reducing auditing costs and accelerating submissions. 
This aligns with their mission of fostering a robust, secure, and scalable Web3 ecosystem through decentralized security solutions​.

## About Hats Audit Competition


Hats Audit Competitions offer a unique and decentralized approach to enhancing the security of web3 projects. Leveraging the large collective expertise of hundreds of skilled auditors, these competitions foster a proactive bug hunting environment to fortify projects before their launch. Unlike traditional security assessments, Hats Audit Competitions operate on a time-based and results-driven model, ensuring that only successful auditors are rewarded for their contributions. This pay-for-results ethos not only allocates budgets more efficiently by paying exclusively for identified vulnerabilities but also retains funds if no issues are discovered. With a streamlined evaluation process, Hats prioritizes quality over quantity by rewarding the first submitter of a vulnerability, thus eliminating duplicate efforts and attracting top talent in web3 auditing. The process embodies Hats Finance's commitment to reducing fees, maintaining project control, and promoting high-quality security assessments, setting a new standard for decentralized security in the web3 space​​.

## Safe Overview

Safe is the account abstraction leader on Ethereum with the most secure smart wallet infrastructure and platform 

## Competition Details


- Type: A public audit competition hosted by Safe
- Duration: 2 weeks
- Maximum Reward: $19,987
- Submissions: 27
- Total Payout: $3,435.77 distributed among 4 participants.

## Scope of Audit

## Project Overview

The project smart contracts in order for Safes to be owned by passkey credentials.

At its core, it implements a Safe v1.3.0+ signature validator that can be used for verifying ES256 WebAuthn credential signatures. It supports using both Solidity based P-256 and EIP-7212 based ECDSA signature verifier implementations.

Additionally, it includes a specialized ERC-4337 signer implementation that uses account storage for the signer configuration (public key and verifier to use) instead of deploying a proxy contract, in order to work around certain ERC-4337 account creation limitations.

## Audit Competition Scope

```
modules/passkey/contracts/
├── 4337
│   ├── README.md
│   └── SafeWebAuthnSharedSigner.sol
├── base
│   └── SignatureValidator.sol
├── interfaces
│   ├── IP256Verifier.sol
│   ├── ISafeSignerFactory.sol
│   └── ISafe.sol
├── libraries
│   ├── ERC1271.sol
│   ├── P256.sol
│   └── WebAuthn.sol
├── SafeWebAuthnSignerFactory.sol
├── SafeWebAuthnSignerProxy.sol
├── SafeWebAuthnSignerSingleton.sol
└── verifiers
    └── FCLP256Verifier.sol
```

**Note that contracts under the `modules/passkey/contracts/vendor` and `modules/passkey/contracts/test` directory are explicitely not in scope for the audit competition.**

Additionally, `modules/passkey/4337/SafeWebAuthnSharedSigner.sol` has not received a prior audit, and would be interesting for participants in the audit competition.

## Low severity issues


- **Event Emission Missing in SafeWebAuthnSharedSigner Configure Function**

  The `SafeWebAuthnSharedSigner::configure` function sets the signer configuration for the calling account but does not emit an event after writing into storage. Initially, the omission was intentional to minimize deployment gas costs. However, it was later decided to implement the event emission, addressing transparency and on-chain state change visibility.


  **Link**: [Issue #3](https://github.com/hats-finance/Safe-0x2909fdefd24a1ced675cb1444918fa766d76bdac/issues/3)


- **Ensure Staticcall Return Value is Checked in `_sha256()` Function**

  The `_sha256()` function, which computes the SHA-256 hash of input bytes, does not check the return value of a low-level `staticcall`. This can cause unexpected behavior if the call fails. It is recommended to explicitly check the return value to ensure proper error handling. A pull request has been made to address this by checking if `staticcall` doesn't revert.


  **Link**: [Issue #14](https://github.com/hats-finance/Safe-0x2909fdefd24a1ced675cb1444918fa766d76bdac/issues/14)


- **Ensure Solidity Pragma Directives Are Fixed to Avoid Floating Versions**

  All contracts have floating pragma directives, which should be fixed to clearly identify the Solidity version for compilation. While the use of floating pragmas in libraries is valid, the inconsistency across contracts suggests a need for aligning on fixed pragmas. The fix has been reconsidered and acknowledged as a valid low-severity find.


  **Link**: [Issue #17](https://github.com/hats-finance/Safe-0x2909fdefd24a1ced675cb1444918fa766d76bdac/issues/17)



## Conclusion

The audit report on Hats.finance highlights a decentralized approach to strengthen the security of web3 projects through audit competitions. These competitions utilize the vast expertise of numerous auditors, fostering a proactive environment for identifying vulnerabilities before project launches. The process is time-based and results-driven, ensuring efficient budget allocation by rewarding only successful findings and eliminating duplicate efforts. One such competition, hosted by Safe, a leading Ethereum account abstraction platform, spanned two weeks with a $19,987 maximum reward. Out of 27 submissions, four participants received a total payout of $3,435.77. The scope included various smart contract components, and low-severity issues were identified and addressed, enhancing transparency and error handling. Overall, Hats.finance's audit competitions effectively reduce auditing costs, enhance project security, and attract top web3 auditing talent, setting a new standard for decentralized security solutions.

## Disclaimer


This report does not assert that the audited contracts are completely secure. Continuous review and comprehensive testing are advised before deploying critical smart contracts.


The Safe audit competition illustrates the collaborative effort in identifying and rectifying potential vulnerabilities, enhancing the overall security and functionality of the platform.


Hats.finance does not provide any guarantee or warranty regarding the security of this project. Smart contract software should be used at the sole risk and responsibility of users.

