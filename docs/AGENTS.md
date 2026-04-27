# AGENTS.md - Agora Personal Digital Sovereignty Base v3.0

## Core Declaration

Agora is a **dual-end collaborative personal digital sovereignty base**. It consists of a mobile end (phone) and a host end (personal computer/server), working together to reclaim every individual's right to define and price their identity, data, computation, and payments.
┌──────────────────────────────┐ ┌──────────────────────────────┐

│ Mobile │ │ Desktop │

│ Sovereignty Control Panel │◄────►│ Service Runtime │

│ The Security Key │ │ The Agent's Home │

│ │ │ │

│ · Master Identity (WebAuthn) │ │ · Steward Child ID Import │

│ · Child ID Derivation │ │ · Policy Sync & Enforcement │

│ · Policy Config (MD/JSON) │ │ · Personal AI Agent Runtime │

│ · Payment Signing (Biometric)│ │ · Service Provider Impl. │

│ · Credential Issuance │ │ · Micro-payments (In-Limit) │

│ · Escalation Approval │ │ · Escalation Requests │

│ · Host Mgmt (Discover/ │ │ · Service Exposure (LAN/WAN) │

│ Auth/Revoke) │ │ │

└──────────────────────────────┘ └──────────────────────────────┘

**The mobile end is the key to the vault. The host end is the worker inside the vault. The key decides who can enter. The worker operates freely within defined limits.**

## 1. Project Philosophy & First Principles

- **Sovereignty over convenience**: Any feature design that sacrifices the user's absolute data or identity control in exchange for convenience is **not allowed**.
- **Verifiable trust**: We do not require users to trust us or any third party. All critical logic must be open-source and auditable, and verifiable through cryptographic means.
- **Protocol as constitution**: The project's governance logic is hard-coded at the protocol layer. Any human intervention or super-administrator privilege is an architectural defect and must be eliminated.
- **Proof of humanity & anti-Sybil**: Master identity creation must bind a unique biometric credential to prevent mass generation of fake identities that pollute governance or exploit incentives.
- **High constraint cost design**: Permission policies are enforced before signing. Violations are blocked preemptively rather than punished afterwards, making the cost of breaking rules far higher than the cost of following them.
- **Cost minimization & market-driven**: Data flows and computation/storage are competitively provided by market-based third-party service providers. Agora serves only as a scheduling layer for trusted identity and payment routing.

## 2. Dual-End Architecture & Module Division

### 2.1 Mobile End Modules (Android / Future iOS)

| Module | Responsibility | Key Interface | Status |
|--------|---------------|---------------|--------|
| Identity | Master identity creation (WebAuthn), child identity derivation (BIP-32), signing | `IdentityManager` | Retained / Enhanced |
| Policy Engine | Permission configuration, conflict detection | `PolicyEnforcer` | Retained |
| Payment | Transaction construction, signing (requires biometric) | `PaymentManager` | Retained |
| Credentials | Credential issuance, verification, QR codes | `CredentialManager` | Retained |
| Vault | Local encrypted storage (optional: keep as emergency backup) | `VaultManager` | Retained (optional) |
| Host Management | Discovery, authorization, communication, revocation of host ends | `HostManager` | **NEW** |
| Service Routing | Remote service calls (forwarding requests to host end) | `RemoteServiceAdapter` | **NEW** |
| Agent API | ~~Removed~~. Agent no longer runs on mobile | - | **REMOVED** |
| UI | Identity, payment, credentials, host management, settings | - | Refactored |

### 2.2 Host End Modules (Compose Desktop / PC)

| Module | Responsibility | Key Interface | Status |
|--------|---------------|---------------|--------|
| Identity | Steward child identity import, local signing | `HostIdentityManager` | **PORTED** |
| Policy Engine | Sync policies from mobile, enforce locally | `PolicyEnforcer` | **PORTED** |
| Payment | Micro-payments (within limits), escalation requests (over-limit) | `HostPaymentManager` | **NEW** |
| Credentials | Credential verification, authorization credential management | `CredentialManager` | **PORTED** |
| Agent Runtime | Personal AI Agent loading, scheduling, monitoring | `AgentRuntime` | **NEW** |
| Service Provider Impl. | Concrete services (AI inference, file storage, data queries) | Implements `ServiceAdapter` | **NEW** |
| Mobile Communication | Pairing, authentication, command receiving, escalation push | `MobileChannel` | **NEW** |
| Service Exposure | HTTP/gRPC endpoints, mDNS broadcasting | `ServiceExposer` | **NEW** |

## 3. Core Interaction Flows

### 3.1 Initial Pairing & Authorization
1. **Host starts** → generates temporary key pair → displays QR code (contains DID + public key + LAN address).
2. **Mobile scans** → gets host info → confirms addition.
3. **Mobile issues authorization credential** → contains steward child DID, policy snapshot, validity period.
4. **Mobile sends credential + encrypted child private key** to host via secure channel (TLS + ECDH).
5. **Host imports** → stores encrypted private key → begins running Agent and services.

### 3.2 Daily Operation
1. **Host Agent** autonomously executes tasks within policy limits (e.g., calling AI services, storing files).
2. When an operation **exceeds limits or permissions**, the host sends an **escalation request** to mobile via push.
3. **Mobile receives notification** → views details → biometric authentication → signs approval → result returned to host.
4. Mobile can **revoke authorization** at any time. Host permissions immediately become invalid.

### 3.3 Service Provider Mode
1. Host can optionally **expose some services** as a "certified service provider" to the Agora network.
2. Other users discover your host services through their mobile ends and settle using the Agora payment module.
3. The service provider child identity's private key is managed by the host. Policies are configured by the service provider themselves.

## 4. Core Codebase Retention List

- The following pure Kotlin modules (no Android dependencies) can be directly reused:

| Module | Files | Adaptation Notes |
|--------|-------|------------------|
| Transaction models | `UnsignedTransaction`, `SignedTransaction` | No changes needed |
| Policy data | `PolicyConfig`, `MessagePolicy`, `PaymentPolicy`, etc. | No changes needed |
| Conflict detection | `PolicyValidator` | No changes needed |
| BIP-32 derivation | `deriveChildKey`, `derivePath` | No changes needed |
| Credential models | `VerifiableCredential`, `Proof`, `CredentialSubject` | No changes needed |
| Crypto utilities | `encrypt`, `decrypt`, `HKDF` | No changes needed |
| Policy enforcer | `PolicyEnforcer` (remove Android Context dependency) | Change to injected storage interface |

**Code that should NOT be retained**:
- All Android-specific UI (Compose code under `ui/` needs rewriting, but layout logic can be referenced)
- Android-specific storage (`EncryptedSharedPreferences`, Room)
- WebAuthn integration (replace with mock or system keychain on desktop)
- `IAgoraAgentService.aidl` (Agent has migrated to host end)

## 5. Current Development Priorities

| Priority | Task | Platform | Description |
|----------|------|----------|-------------|
| **P0** | Set up Compose Desktop project | Host | Run basic window, display "Agora Host Started" |
| **P0** | Port core codebase | Shared | Copy retained pure Kotlin files to new project |
| **P1** | Implement host identity import | Host | Receive and store encrypted child identity from mobile |
| **P1** | Implement mobile communication module | Host | QR display, HTTP endpoints, escalation push |
| **P1** | Implement mobile host management UI | Mobile | Scan to add host, view status, authorize/revoke |
| **P2** | Implement Agent runtime | Host | Local LLM or API calls, policy-constrained |
| **P2** | Implement service exposure | Host | Implement an example service adapter (e.g., DeepSeek mock) |

## 6. File Structure
- Agora-v3/

├── shared/ # Shared pure Kotlin library
│ ├── crypto/ # Encryption, signing, derivation
│ ├── policy/ # Policy models & validation
│ ├── payment/ # Transaction models
│ ├── credential/ # Credential models
│ └── vault/ # Vault encryption/decryption
├── desktop/ # Host end (Compose Desktop)
│ ├── identity/ # Identity import
│ ├── agent/ # Agent runtime
│ ├── service/ # Service provider implementation
│ ├── channel/ # Mobile communication
│ └── ui/ # Desktop UI
├── mobile/ # Mobile end (Android, future)
│ ├── identity/ # Identity creation
│ ├── host/ # Host management
│ ├── payment/ # Payment signing
│ └── ui/ # Compose UI
├── docs/ # All .md specification documents
│ ├── AGENTS.md
│ ├── PROJECT_OVERVIEW.md
│ ├── BUILD.md
│ ├── *_SPEC.md
│ └── ...
└── application（agora android）_build_checklist.md

## 7. Build & Run

### Host End (Compose Desktop)

```bash
cd desktop
./gradlew run
```

- Shared Library
```bash
cd shared
./gradlew build
```

Mobile End (Android, deferred)
Keep the existing agora0.1.3-android repository. Sync and update after the host end is operational.

## 8. Development Conventions for AI Collaborators (Must Follow)
- Unambiguous instructions: When generating code or modifying documents, pursue mathematical precision.

- Security red lines: Any modification involving cryptographic algorithms must include a corresponding security proof description or reference a reputable security audit report. Backdoors, hardcoded keys, or disabling certificate verification for debugging convenience are absolutely prohibited.

- Context awareness: In generated code comments, clearly indicate the module's position and role in the overall sovereignty architecture.

- Document synchronization: When modifying core logic, simultaneously update README.md (user-facing) and this document AGENTS.md (developer/AI-facing).

- Critical comment requirements:

- Biometric registration functions: // Proof-of-humanity anti-Sybil verification, prevents master identity abuse

- Policy verification functions: // Preemptive blocking mechanism, enforced before signing, raises violation cost

- BIP-32 derivation functions: // Follows BIP-32 spec, hardened derivation path, child private keys independently usable

- Transaction signing functions: // Signature covers normalized JSON sorted by key, prevents signature malleability

- Private key storage: // WARNING: DEMO ENVIRONMENT ONLY! Production must never store plaintext private keys

## 9. Module Integration & Completeness Checklist

- Before delivery, verify the following flows work correctly:

- Mobile: Master identity creation → WebAuthn registration successful → first default child identity auto-generated

- Mobile: Child identity creation → derivation path auto-assigned → unique identifier code generated → default permission config associated

- Mobile: Host management → scan QR code → authorization credential issued → host appears in list

- Host: Startup → QR code displayed → receives authorization → imports steward child identity → Agent starts

- Host: Agent payment within limits → auto-signed and executed

- Host: Agent payment over limit → escalation request pushed to mobile → mobile approves with biometric → transaction completed

- Mobile: Revoke host authorization → host permissions immediately disabled

---
- This document is the architectural constitution of Agora v3.0. Any implementation deviation must first update this document.
