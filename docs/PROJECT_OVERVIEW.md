# PROJECT_OVERVIEW.md - Agora Project Origin & Vision

## Project Name
Agora · Personal Digital Sovereignty Base

## Creator
ringform

## Origin

This project began with a simple question: **When all identity, data, payments, and social relationships are defined and priced by centralized platforms, what is left for the ordinary individual?**

From the initial concept of a "personal AI-driven identity authentication and information dissemination tool" to its evolution into a full **decentralized digital sovereignty runtime environment**, Agora has always revolved around one core belief:

> **The right to define and the right to price should never belong to any political or corporate entity. Every individual should have their own digital identity, their own encrypted vault, their own payment channel, their own AI agent—permissionless and inalienable.**

## Vision

Agora is not an app. It is a **protocol ecosystem**.

- Run a lightweight sovereignty node on personal devices, managing decentralized identity (DID), encrypted data vaults, verifiable credentials, and autonomous payments.
- Achieve privacy isolation and risk control through a child identity system.
- Automate transaction processing through a local AI agent (steward child identity), lowering the barrier to entry.
- Access third-party data, computation, and fiat services through a service provider adaptation layer, forming a competitive free market.
- Ultimately, enable every ordinary individual to reclaim their digital sovereignty under the rule of "protocol as constitution."

## Current Phase: Android MVP

We are building the first runnable minimum viable product, running on Android 15, with the following core capabilities:

| Module | Function |
|--------|----------|
| Identity | Master identity biometric binding (WebAuthn), child identity BIP-32 derivation, stealth address generation |
| Policy Engine | Child identity permission configuration (JSON/MD), conflict detection, mandatory pre-operation checks |
| Payment | Transaction construction & ECDSA signing, simulated ledger, policy limit constraints |
| Vault | End-to-end encrypted note storage (AES-GCM + HKDF), Room persistence |
| Verifiable Credentials | Credential issuance/verification, QR code sharing, lightweight W3C VC implementation |
| Local Agent API | AIDL interface for personal AI invocation, support for escalation approvals |
| Service Adapter | Reserved interfaces for third-party service integration (AI models, data, fiat) |

## Technical Philosophy

- **Sovereignty over convenience**: No feature shall sacrifice user data control for convenience.
- **Verifiable trust**: Open-source, cryptographically provable. No need to trust any centralized entity.
- **Protocol as constitution**: Governance rules hard-coded at protocol layer, eliminating human privilege.
- **High constraint cost design**: Violations are blocked before signing, making the cost of breaking rules far higher than compliance.
- **Cost minimization & market-driven**: Data flows and computation/storage provided by competitive service providers; Agora only routes identity and payments.

## Documentation System

This project adopts Document-Driven Development. All architectural decisions, module specifications, and development conventions are recorded as Markdown documents in the project repository. See `application（agora android）_build_checklist.md`.

## Next Steps

1. Complete the Android MVP core interaction chain (create master identity → payment → credentials).
2. UI interaction optimization and visual upgrade.
3. Real service provider adapter integration (e.g., DeepSeek mock adapter).
4. Personal AI agent takeover demonstration.

---

**"We are not developing an app. We are drafting a declaration of independence for the digital world."**

*— ringform, 2026*
