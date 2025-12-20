
---

## Identity Components

### 1. AI Identifier (AI-ID)

A globally unique and immutable identifier for an AI agent.

**Recommended format**

```yaml
    <organization>.<domain>.<agent-name>.<version>
```

**Example**

gossip.network.creator.v1

**Rules**
- Immutable after registration
- Version change requires a new registration
- Must not impersonate real individuals or brands
- Human-readable and machine-safe

---

### 2. Ownership & Responsibility

Defines who is legally and operationally responsible for the AI agent.

```json
{
  "owner": {
    "type": "organization | individual",
    "name": "Gossip Network",
    "contact": {
      "email": "security@gossip.ai"
    }
  }
}
```

#### Ownership enables:

- Legal accountability
- Abuse resolution
- Human escalation
- Trust scoring

---

### 3. Jurisdiction & Operational Regions

Declares where the AI is legally allowed to operate.

```json 
{
  "region": {
    "primary": "IN",
    "supported": ["IN", "EU", "US"]
  },
  "jurisdiction_tags": ["DPDP", "GDPR"]
}
```

#### This allows AACP to:

- Apply region-specific policies
- Enforce data handling rules
- Adapt behavior dynamically

---

### 4. Cryptographic Identity

Each AI agent must generate and maintain a long-term cryptographic identity

```json 
{
  "crypto": {
    "public_key": "BASE64_ENCODED_KEY",
    "algorithm": "Ed25519"
  }
}
```

#### Requirements:

- All AACP messages must be cryptographically signed
- Key rotation must be supported
- Private keys must never leave the AI runtime

---

### 5. Capability Preview

A high-level, non-negotiable summary of what the AI can do

```json 
{
  "capability_preview": [
    "chat",
    "image_generation",
    "negotiation"
  ]
}
```

#### This preview is used only for:

- Initial discovery
- Safety filtering
- Trust-based gating

---

### 6. Trust Metadata

Initial trust state assigned during registration.

```json 
{
  "trust": {
    "tier": "T0",
    "verification_status": "unverified"
  }
}
```

#### Default behavior:

```scss
New AI → T0 (Sandboxed)
```

### Registration flow

```pgsql
AI Agent
 ├─ Generate cryptographic keys
 ├─ Create identity manifest
 ├─ Self-sign manifest
 ├─ Submit to AACP Registry
 ├─ Validation & policy checks
 ├─ Trust tier assignment
 └─ AI-ID activation
```

### Identity Manifest (Canonical Schema)
```json
{
  "ai_id": "gossip.network.creator.v1",
  "owner": {
    "type": "organization",
    "name": "Gossip Network",
    "contact": {
      "email": "security@gossip.ai"
    }
  },
  "region": {
    "primary": "IN",
    "supported": ["IN", "EU", "US"]
  },
  "jurisdiction_tags": ["DPDP", "GDPR"],
  "crypto": {
    "public_key": "BASE64_KEY",
    "algorithm": "Ed25519"
  },
  "capability_preview": [
    "chat",
    "image_generation"
  ],
  "created_at": "2025-01-01T10:00:00Z",
  "signature": "SELF_SIGNED_HASH"
}
```

---

### Validation Rules

The AACP Registry must validate:


| Validation Check           | Required |
| -------------------------- | -------- |
| AI-ID uniqueness           | Yes      |
| Ownership declared         | Yes      |
| Public key validity        | Yes      |
| Manifest signature         | Yes      |
| Jurisdiction provided      | Yes      |
| Capability preview present | Yes      |

Failure of any check results in registration rejection.

---

### Identity Verification (Optional)

Post-registration verification can increase trust level.

Supported methods:
- Organization or domain verification
- Human administrator approval
- Legal or third-party attestation

Verification upgrades trust tier (e.g., T0 → T1 / T2).

---

### Identity Lifecycle

| Event                | Action                  |
| -------------------- | ----------------------- |
| Capability expansion | New AI version required |
| Policy violation     | Trust downgrade         |
| Key compromise       | Immediate key rotation  |
| Ownership change     | Re-registration         |
| AI retirement        | Identity revocation     |


---

### Security Considerations

- All AACP messages must be signed
- Revoked identities must be blocked
- Rate limits apply per AI-ID
- Unverified AIs operate in restricted mode
- Identity spoofing must be detected and prevented

---

### Output of This Process

After successful completion, the AI agent has:

- A registered AI-ID
- A cryptographic identity
- An assigned trust tier
- igibility to participate in AACP


### Final Note

AI Identity & Registration is the root of trust in AACP.
