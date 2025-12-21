## Intent

```psql 
Intent
├─ Intent ID
├─ Action
├─ Domain
├─ Purpose
├─ Risk Level
├─ Constraints
├─ Duration
└─ Accountability
```
---

## Intent Declaration

### Intent Declaration Schema

```json
{
  "intent_id": "INT-2025-00921",
  "action": "image_generation",
  "capability_id": "image_generation.basic",
  "domain": "marketing",
  "purpose": "Create product banner for social media",
  "risk_level": "medium",
  "requested_constraints": {
    "no_faces": true,
    "audience": "India"
  },
  "duration": "single_execution"
}
```

### Rules

- Intent ID must be unique
- Action must map to a discovered capability
- isk level must be declared honestly
- Missing fields → rejection

---

### Negotiation Flow

```cpp
Requesting AI
 ├─ Submits intent
 ↓
Responding AI
 ├─ Evaluates intent
 ├─ Applies policy & trust checks
 ├─ Accepts / Modifies / Rejects
 ↓
Negotiation (optional)
 ↓
Permission Granted or Denied
```

## Step-by-Step Process

### Step 1: Intent Submission

The requesting AI submits a signed intent declaration.

```json
{
  "type": "INTENT_REQUEST",
  "from_ai": "gossip.network.orchestrator.v1",
  "intent": { ... }
}
```

Unsigned or malformed intents must be rejected.

---

### Step 2: Policy & Trust Evaluation

The responding AI evaluates:

- Trust tier of requester
- Risk level of intent
- risdiction compatibility
- Internal and global policies

Example outcome:

```json
{
  "evaluation_result": "MODIFY",
  "reason": "Medium-risk intent from T1 AI"
}
```
---

### Step 3: Constraint Negotiation (Optional)

The responding AI may modify constraints.

```json
{
  "type": "INTENT_COUNTER",
  "modified_constraints": {
    "no_faces": true,
    "max_creativity": 0.5,
    "disclaimer_required": true
  }
}
```

The requesting AI must explicitly accept modified constraints.

---

### Step 4: Permission Decision

Final permission response

```json
{
  "type": "INTENT_RESPONSE",
  "intent_id": "INT-2025-00921",
  "decision": "APPROVED",
  "granted_constraints": {
    "no_faces": true,
    "max_creativity": 0.5
  },
  "permission_token": "PERM-88291",
  "expires_at": "2025-01-01T10:30:00Z"
}
```

### Permission Token

A Permission Token:

- Binds intent to execution
- Is time-bound
- Is non-transferable
- Must be presented in execution requests

Without a valid token → execution denied

---

### Failure Scenarios

| Scenario            | Response           |
| ------------------- | ------------------ |
| Capability mismatch | Reject             |
| Missing intent      | Reject             |
| Trust too low       | Reject or restrict |
| Policy violation    | Reject             |
| Expired permission  | Deny execution     |

---

### Security Considerations

- All intents must be signed
- Permission tokens must be verifiable
- Replay attacks must be prevented
- Negotiation logs must be immutable
- Rate limits apply per AI-ID

### Audit & Logging

Each intent negotiation generates:

- Intent record
- Policy decision trace
- Granted constraints
- Permission token hash

These logs must be:

- Tamper-resistant
- Time-stamped
- Retained per policy

### Output of This Process

After successful completion:

- Intent is mutually agreed
- Constraints are finalized
- Permission token is issued

AI is eligible to execute the action