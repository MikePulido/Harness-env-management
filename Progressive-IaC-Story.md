# Application Protection During Infrastructure Changes
## Executive Summary

### The Problem
**Infrastructure changes can break production applications.** Companies lack a way to protect deployed workloads from the potential downstream impact of infrastructure upgrades.

### Why This Matters
- **Infrastructure changes can cause application incidents:** Successful infrastructure upgrades may break applications that depend on them
- **All workloads impacted simultaneously:** No progressive exposure—every application potentially affected at once
- **Application compatibility unknown until production:** No way to verify workloads will remain healthy after infrastructure changes
- **Reactive incident response:** Teams may need to respond to broken applications instead of proactively protecting them

### The Gap
| What Harness Has | What's Missing |
|-------|---------|
| **IaCM:** Manages infrastructure changes | No protection for applications that may be affected |
| **CD:** Deploys applications progressively | Can't progressively expose applications to infrastructure changes |
| **CV:** Verifies application health | No verification during infrastructure changes |

**Gap:** Infrastructure changes and application deployments are managed separately. No way to protect applications from potential infrastructure impacts.

---

### The Solution
**Progressive exposure of applications to infrastructure changes with automated verification.**

Bridge IaCM and CD to protect workloads:
- Progressive migration of applications to changed infrastructure using bluegreen and canary deployment strategies.
- Continuous verification of application health during infrastructure changes
- Automated rollback when applications show degradation

---

### Competitive Advantage
**Harness is the only platform with visibility into both infrastructure AND applications.**

- Infrastructure tools lack application awareness
- Application tools can't orchestrate infrastructure changes
- No competitor bridges both layers

---

### Customer Value
- Protect production applications from potential infrastructure impacts
- Reduce risk of application incidents during infrastructure upgrades
- Accelerate infrastructure security patches with confidence in workload health
- Proactive verification instead of reactive incident response

---

### Recommendation
**Build application protection for infrastructure changes as unified IaCM + CD capability.**

Leverage Harness's unique position with both infrastructure management and application deployment to deliver automated workload protection during infrastructure changes.

---

## Use Case: EKS Forced Kubernetes Version Upgrade

### The Scenario
AWS announces Kubernetes 1.28 end-of-support. A company running 200 microservices on EKS must upgrade to 1.29 within the deprecation window or face forced upgrades.

**Current State (Without Application Protection):**

```
Timeline:
Day 1: EKS control plane upgraded to 1.29 (AWS managed)
Day 2-3: Platform team upgrades all node groups to 1.29
Day 3: All 200 microservices now running on K8s 1.29

Impact:
- 15 applications experience errors due to deprecated API usage
- All applications were affected simultaneously when nodes upgraded
- 4-hour incident response to identify and fix broken services
- Some issues only appeared under production traffic load
- No automated rollback - manual pod restarts and config changes required
```

**With Application Protection:**

```
Timeline:
Day 1: EKS control plane upgraded to 1.29 (AWS managed)
Day 2: Create new node group with K8s 1.29
Day 2: Migrate 10% of applications (20 services) to new nodes
       → Continuous Verification detects 3 services with errors
       → Automated rollback moves those 3 services back to old nodes
       → 197 services unaffected
Day 3: Fix 3 broken services, re-test
Day 4: Progressive migration continues: 25% → 50% → 100%
Day 7: All services migrated with zero production incidents

Impact:
- 3 applications experienced errors (detected in 10% canary)
- 197 applications protected from potential issues
- Issues caught early with 10% exposure, not 100%
- Automated rollback prevented extended outages
- Controlled timeline with verification at each step
```

### The Value
**Blast radius management:** 10% of apps exposed first, not 100%
**Automated detection:** Continuous Verification catches issues immediately
**Automatic rollback:** Problem apps returned to working state without manual intervention
**Production confidence:** Safe path to required K8s upgrade without "big bang" risk

This pattern applies to any forced infrastructure change: database version upgrades, middleware updates, security patches.
