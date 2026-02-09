# Managing Blast Radius of Environment-Wide Infrastructure Changes

## The Problem

When you upgrade shared infrastructure (e.g., Kubernetes version), **every application in that environment is exposed at once.** There's no progressive rollout for infrastructure changes the way there is for application deployments.

**The core question:** *How do I upgrade my Kubernetes version and ensure all my deployed services are unaffected?*

## The Gap

Harness has the pieces but they're disconnected:

- **IaCM** manages infrastructure changes but has no visibility into application health
- **CD** does progressive rollouts (canary/blue-green) but only for app deployments, not infra changes
- **CV** verifies health but isn't triggered by infrastructure events

**No one orchestrates environment-wide progressive exposure of applications to infrastructure changes.**

## The Solution

**Environment-level progressive rollout for infrastructure changes** — apply canary/blue-green patterns not to a single app deployment, but to the entire environment's workloads as infrastructure changes roll out underneath them.

Example — EKS upgrade from 1.28 → 1.29:

1. Stand up new node group on 1.29
2. Migrate 10% of workloads → CV validates health
3. Issues detected? Automated rollback to old nodes. No issues? Continue.
4. 25% → 50% → 100%, verified at each stage

**Blast radius goes from 100% on day one to 10% in a controlled canary.**

## Why Harness

No other platform has visibility into both the infrastructure layer *and* the application layer. Terraform can upgrade your cluster. Argo can deploy your apps. Neither can progressively migrate workloads across infrastructure changes while verifying health — that requires bridging IaCM + CD + CV.

## Customer Value

- **Blast radius control** for environment-wide infra changes
- **Automated verification** at each migration stage
- **Automated rollback** when degradation is detected
- **Confidence to move fast** on forced upgrades, security patches, and platform modernization

---

This pattern applies to any shared infrastructure change: K8s upgrades, database engine versions, node OS patches, service mesh upgrades, etc.
