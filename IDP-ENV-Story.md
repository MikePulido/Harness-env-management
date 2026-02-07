# Self-Service Integration Environments
## Executive Summary

### The Problem
Developers discover integration issues after merging to shared dev environments, causing delays and broken environments for all teams.

### Why This Matters
- Integration issues found after merge, not before
- Multiple concurrent PRs break shared dev environments
- Platform teams manually provision test environments
- Developers context-switch while waiting for fixes

### The Gap
| What Harness Has | What's Missing |
|-------|---------|
| **IDP:** Developer self-service portal | No ephemeral integration environments |
| **IaCM:** Infrastructure provisioning | No automated PR environment creation |
| **CD:** Application deployment | Can't deploy PR + dependencies in isolation |
| **CV:** Health verification | No pre-merge integration testing |

**Gap:** No self-service way to test integration before merge.

---

### The Solution
**IDP self-service ephemeral environments with namespace isolation.**

- Developers request via IDP portal
- IaCM provisions namespace-scoped environment
- CD deploys PR code + dependencies
- CV runs automated tests
- Auto-teardown after merge

---

### Competitive Advantage
- Uffizzi/Okteto: No IDP self-service integration
- Port/Backstage: No ephemeral environment orchestration
- Vercel/Netlify: Frontend-only
- **Harness:** IDP + IaCM + CD + CV integrated

---

### Customer Value
- Accelerate time to production through earlier issue detection
- Integration testing before merge prevents shared environment breakage
- Cost-effective namespace isolation vs full environment provisioning
- Self-service eliminates platform bottleneck and reduces manual toil

---

### Recommendation
Build self-service integration environments as IDP capability using namespace isolation for cost-effective, high-velocity pre-merge testing.

---

## Use Case: Microservices Team

**Scenario:** 50 microservices, 100 PRs/week, shared dev breaks frequently

**Before:**
```
5 days: Code → merge → discover issue → fix → re-merge
2 context switches per PR
```

**After:**
```
2 days: Code → test in isolated env → fix → merge clean
0 context switches
```

**Impact:**
- Significantly faster time to merge
- Reduced developer context switching
- Stable shared environments
