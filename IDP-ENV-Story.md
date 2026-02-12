# Self-Service Integration Environments

## The Problem

Developers discover integration issues **after merging** to shared dev environments, breaking those environments for everyone. Platform teams manually provision test environments, creating bottlenecks. In complex Kubernetes microservice architectures, it becomes difficult to have a local environment to write code that has consistencies with higher environments. This can take days to fix issues that could be caught in real time.

## The Solution

**IDP-driven ephemeral environments with namespace isolation.**

1. Developer requests environment via IDP portal
2. IaCM provisions namespace-scoped environment
3. CD deploys PR code + its dependencies in isolation
4. CV runs integration tests
5. Auto-teardown after merge

## Why Harness

**Harness uniquely integrates IDP + IaCM + CD** to deliver the full workflow.

## Customer Value

- **Shift integration left** — catch issues before merge, not after
- **Protect shared environments** from concurrent PR breakage
- **Eliminate platform bottleneck** with developer self-service
- **Cost-effective** namespace isolation vs. full environment clones
