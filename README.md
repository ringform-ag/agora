# Agora · Personal Digital Sovereignty Base

> **The information revolution has arrived. But who seized its fruits?**

## A Revolution, A Paradox

The internet was supposed to liberate every individual. It promised free connection, infinite knowledge, and universal creation. Yet half a century later, this is our reality:

- **Data is worth more than oil, but those who produce it earn nothing.**
- **AI understands you better than you understand yourself, but you don't control it.**
- **Connectivity is everywhere, yet every node is a surveillance camera.**

This is not the failure of the information revolution. This is the result of its **fruits being stolen**.

The rightful order should be: whoever produces the data gets to decide. Whoever does the computing gets to benefit. Not every click, every photo, every conversation you make becoming an entry on someone else's balance sheet.

## The Collapse of Privacy: Not Just Leaks, but Systemic Design Flaws

| Event | Scale | Date |
|:---|:---|:---|
| Global Email Password Breach | **184 million** records exposed | 2025 |
| French Patient Data Theft | **15.8 million** patient records leaked on the dark web, including sensitive notes on political figures | Feb 2026 |
| US Healthcare Data Breach | Over **6 million** Social Security Numbers stolen | 2026 |
| French Telecom FREE MOBILE Fined | CNIL fines totaling **€42 million** | Jan 2026 |

But that's not the worst part.

**Platforms are actively surveilling you.** Meta secretly hijacked browser cookies and commands on Android phones to monitor users' web browsing, even in incognito mode. When you share your location on Instagram's Friend Map, that data stream directly exposes your real-time location and social network, blurring the line between digital risk and physical threat. Google, Meta, Amazon—these giants make hundreds of billions of dollars from your data every year. Your reward? A "User Agreement" you've never actually read.

**AI is weaponizing your data.** In 2025, criminals used static photos to synthesize dynamic videos that bypassed WeChat facial verification, draining bank accounts. In Hangzhou, China, two individuals were convicted of using AI "face-swapping" technology to steal and resell personal information, ordered to pay public interest damages. From AI face-swapping "rich, beautiful women" for romance scams worth 130,000 yuan, to AI-altered voices impersonating "grandsons" to defraud the elderly, to AI-generated voices pretending to be women to solicit money—these are real crimes happening right now, fueled by countless personal records hoarded in underground databases.

**You "agreed" to all those terms? That was coerced.** In 2025, a Chinese court found that a dictionary app would exit immediately and offer no service when a user rejected its privacy policy—"disagree, and you can't use it." The court ruled this as **forced personal information collection**. This is not just one app's problem. It is the design of the entire digital economy: the word "Agree" masks a carefully engineered dilemma of **"surrender your data, or leave civilization."**

## The Root Cause: Centralization

All of these problems trace back to a single technical architecture: **Centralization**.

- Identity is assigned by centralized platforms. They can revoke you at any time.
- Data is stored on someone else's servers. They can analyze it, auction it, leak it at will.
- AI agents run on someone else's computers. Their work logs, your preferences, your secrets—all under someone else's watch.

Centralization means there is a single point—a single controller, a single point of failure, a single beneficiary. And that single point is **not you**.

## The Solution: Agora

Agora is an open-source personal digital sovereignty base, built on a dual-end collaborative architecture consisting of a mobile end (phone) and a host end (PC).

┌──────────────────────────────┐ ┌──────────────────────────────┐

│ Mobile │ │ Desktop │

│ Sovereignty Control Panel │◄────►│ Service Runtime │

│ The Security Key │ │ The Agent's Home │

│ │ │ │

│ · Master Identity (WebAuthn) │ │ · Steward Child ID Import │

│ · Child ID Derivation (BIP-32)│ │ · Policy Sync & Enforcement │

│ · Policy Config (MD/JSON) │ │ · Personal AI Agent Runtime │

│ · Payment Signing (Biometric)│ │ · Service Provider Impl. │

│ · Credential Issuance │ │ · Micro-payments (In-Limit) │

│ · Escalation Approval │ │ · Escalation Requests │

│ · Host Mgmt (Discover/Auth/Revoke)│ │ · Service Exposure (LAN/WAN) │

└──────────────────────────────┘ └──────────────────────────────┘

- **Define your own identity**: No phone number. No email. Create a digital identity (DID) controlled only by you using your fingerprint or face, and derive countless privacy-isolated sub-identities.
- **Control your own data**: Your notes, credentials, transaction records are end-to-end encrypted and stored on your own devices. No one can decrypt them, including us.
- **Decide your own payments**: Built-in sovereign payment module. Every transaction is signed by your private key and constrained by the policy limits you preset. No bank can freeze it. No platform can take a cut.
- **Run your own AI**: Your personal AI agent runs on your own computer, processing tasks autonomously with a child identity you authorized. It works for you, not to collect data for megacorps.

Agora does not own you. It is merely a sovereign hand you extend into the digital world.

## Technical Features

- **Decentralized Identity (DID)**: W3C standard, self-generated, no registration center required.
- **Biometric Authentication**: WebAuthn bound, used to prove "you are a real person", not to harvest your biometric data.
- **Child Identity System**: BIP-32 hierarchical derivation. One master identity generates countless privacy-isolated sub-identities for different scenarios, preventing tracking.
- **End-to-End Encryption**: AES-256-GCM. Keys never leave your device.
- **Verifiable Credentials**: Lightweight W3C VC implementation for authorizing third-party services and proving identity attributes.
- **Policy Engine**: MD/JSON permission configuration. Mandatory check before signing. Violations blocked preemptively.
- **Sovereign Payments**: ECDSA transaction signing, simulated ledger verification, with reserved multi-payment-channel adapters.

## Status

🚧 **Early development stage**. The first Android MVP has been built, and the core cryptographic chain is operational. Currently refactoring towards a Compose Multiplatform dual-end architecture.

## Why Open Source

Because we believe:

> **The right to define and the right to price should never belong to any political or corporate entity. Every individual should have their own digital identity, their own encrypted vault, their own payment channel, their own AI agent—permissionless and inalienable.**

This is not just an app. This is a declaration of independence for the digital world.

## Join Us

- Read the [Project Overview](docs/PROJECT_OVERVIEW.md)
- Check the [Architecture Documentation](docs/AGENTS.md)
- Submit an Issue or Pull Request to ask questions or contribute code

---

**Agora — Take back your digital sovereignty.**
