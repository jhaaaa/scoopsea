# Scoopsea

An anonymous whistleblower marketplace where insiders sell verified information to journalists and investigators via encrypted channels. Sellers prove access without revealing identity. Buyers escrow payment. Reputation accrues to pseudonyms, not people.

## Why this can't exist anywhere else

- Centralized platforms won't build it (legal liability)
- Public blockchains can't (not private enough)
- Signal can't (no payment rails, no identity layer, no reputation)
- XMTP + smart contracts + ZK proofs can

## The primitives

- **XMTP/Convos** — E2E encrypted messaging with per-conversation identity. No cross-conversation linkability. No server-side access to content.
- **OpenClaw** — AI agent as marketplace moderator, dispute mediator, proof verifier, reputation tracker. Neutral third party running open-source logic inside encrypted channels.
- **ZK proofs** — Prove employment, access, or credentials without revealing identity. "This person works at TechCorp engineering" without revealing which employee.
- **Smart contract escrow** — Payment held until buyer confirms delivery. Trustless exchange between anonymous parties.

## The demo flow

### Act 1 — The Seller

Alice works at TechCorp. She has internal Slack logs showing executives knew about a security breach months before disclosure. She opens Scoopsea, uploads proof of employment (ZK proof from her @techcorp.com email — proves domain access without revealing which address). Posts a listing under a pseudonym: "$5k for internal comms showing prior knowledge of the breach."

### Act 2 — The Buyer

Bob is a journalist. He browses listings, verifies Alice's ZK proof (valid: seller really works at TechCorp engineering). Clicks buy. Smart contract escrows $5k. Bob and Alice are matched into a private encrypted XMTP DM. Alice delivers the documents (encrypted, watermarked with Bob's key for leak traceability). Bob verifies, releases payment. Both rate each other.

### Act 3 — Reputation compounds

Two months later, Alice posts another leak under the same pseudonym. A different journalist sees: "This seller delivered solid TechCorp intel before — 5-star rating, 1 successful deal." Reputation is working. Meanwhile, Alice sells leaks about other companies under different pseudonyms. Per-conversation identity means no one can connect the dots. She's built a portfolio of reliable insider identities without ever revealing she's the common thread.

## Architecture (high level)

```
┌─────────────────────────────────────────────────┐
│                  Scoopsea App                    │
│           (marketplace frontend)                 │
│                                                  │
│  ┌──────────┐  ┌──────────┐  ┌───────────────┐  │
│  │ Listings │  │ Profiles │  │  ZK Proof      │  │
│  │ & Search │  │ & Reputation│ │  Verification │  │
│  └────┬─────┘  └─────┬────┘  └───────┬───────┘  │
│       │              │               │           │
├───────┼──────────────┼───────────────┼───────────┤
│       │         XMTP Layer           │           │
│       │    (encrypted messaging)     │           │
│  ┌────┴──────────────┴───────────────┴────────┐  │
│  │  Per-conversation identity                 │  │
│  │  E2E encrypted DMs (document exchange)     │  │
│  │  No server-side content access             │  │
│  └────────────────┬───────────────────────────┘  │
│                   │                              │
├───────────────────┼──────────────────────────────┤
│            OpenClaw Agent                        │
│  ┌────────────────┴───────────────────────────┐  │
│  │  Marketplace moderation                    │  │
│  │  ZK proof validation                       │  │
│  │  Dispute mediation                         │  │
│  │  Reputation scoring                        │  │
│  │  Buyer/seller matching                     │  │
│  └────────────────┬───────────────────────────┘  │
│                   │                              │
├───────────────────┼──────────────────────────────┤
│           Smart Contracts                        │
│  ┌────────────────┴───────────────────────────┐  │
│  │  Payment escrow                            │  │
│  │  Dispute resolution                        │  │
│  │  Reputation registry (on-chain)            │  │
│  └────────────────────────────────────────────┘  │
│                                                  │
├──────────────────────────────────────────────────┤
│            ZK Proof System                       │
│  ┌────────────────────────────────────────────┐  │
│  │  ZK Email (prove @domain.com control)      │  │
│  │  Employment attestations                   │  │
│  │  Credential verification                   │  │
│  └────────────────────────────────────────────┘  │
└─────────────────────────────────────────────────┘
```

## Open questions

- Legal framework: Which jurisdictions? Whistleblower protection laws vary wildly.
- ZK proof fidelity: What level of proof is "enough" for buyers to trust?
- Document watermarking: How to make leak traceability robust without compromising seller privacy?
- Reputation cold start: How does a new seller with zero history get their first deal?
- Moderation: What listings should the agent refuse? (National security? Personal grudges?)
- Economics: Fee structure? Platform take? Who pays gas?

## What Thiel would ask

"What's your unfair advantage?"

Answer: We're building the market that incumbents can't build. The New York Times can't build this (legal liability). Facebook can't (privacy). Even Signal can't (no payment rails, no identity, no reputation). XMTP + smart contracts + ZK proofs can. We're not competing with existing platforms. We're creating a market that doesn't exist because the infrastructure didn't exist. Zero to one.
