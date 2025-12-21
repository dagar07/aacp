## Capability Model


This process focuses on the **Capability Descriptor** level.

---

## Capability Descriptor

A **Capability Descriptor** defines what an AI *can* do under specific conditions.

### Example Descriptor

```json
{
  "capability_id": "image_generation.basic",
  "description": "Generate non-photorealistic images",
  "domains": ["marketing", "education"],
  "risk_level": "medium",
  "requires_verification": false,
  "restricted_regions": [],
  "supported_formats": ["png", "jpg"]
}
```

---

### Discovery Flow

```pgsql
Requesting AI
 ├─ Declares identity
 ├─ Declares intent
 ├─ Requests discovery
 ↓
AACP Policy Layer
 ├─ Validates trust tier
 ├─ Applies regional rules
 ├─ Filters capabilities
 ↓
Responding AI
 └─ Returns permitted capabilities

```

---

### Step-by-Step Process
---

### Step 1: Discovery Request

The requesting AI initiates discovery with identity and intent.

```json
{
  "type": "CAPABILITY_DISCOVERY_REQUEST",
  "from_ai": "gossip.network.orchestrator.v1",
  "intent": {
    "purpose": "content_creation",
    "domain": "marketing",
    "risk_level": "medium"
  }
}
```
Requests without intent must be rejected

---

### Step 2: Trust & Policy Evaluation

Before exposing any capability, the responding AI (via AACP) evaluates:

- Requesting AI’s trust tier
- Jurisdiction compatibility
- Risk level of requested domain
- Local and global policies

Example decision:

```json
{
  "policy_decision": "ALLOW_PARTIAL",
  "reason": "Unverified AI requesting medium-risk capabilities"
}
```
---

### Step 3: Capability Filtering

Capabilities are filtered based on:
- Trust tier
- Region and law
- Declared intent
- AI’s own policies

| Trust Tier | Exposure           |
| ---------- | ------------------ |
| T0         | Minimal, safe-only |
| T1         | Standard           |
| T2         | Extended           |
| T3         | Full               |

---

### Step 4: Discovery Response

The responding AI returns only permitted capabilities.

```json
{
  "type": "CAPABILITY_DISCOVERY_RESPONSE",
  "to_ai": "gossip.network.orchestrator.v1",
  "capabilities": [
    {
      "capability_id": "image_generation.basic",
      "risk_level": "medium",
      "constraints": {
        "no_faces": true,
        "max_creativity": 0.6
      }
    }
  ]
}
```
---

### Capability Constraints

Capabilities may include constraints such as:

- Region restrictions
- Content limitations
- Rate limits
- Required disclaimers
- Mandatory human approval

Constraints are binding and enforced in later processes.

---

### Security Considerations

- Discovery responses must be signed
- No execution access is granted at this stage
- Rate limits apply per AI-ID
- Discovery requests are logged and auditable

---

### Failure Scenarios

| Scenario           | Response                        |
| ------------------ | ------------------------------- |
| Missing intent     | Reject                          |
| Insufficient trust | Return limited capabilities     |
| Region conflict    | Exclude restricted capabilities |
| Policy violation   | Reject discovery                |

--- 

### Output of This Process

After completing Capability Discovery, the requesting AI has:

- A filtered list of available capabilities
- Associated constraints and risk levels
- No execution permission yet

####  Capability Discovery is the safety valve of AACP.
It ensures AI agents never overreach, over-assume, or over-trust.