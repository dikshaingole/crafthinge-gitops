# crafthinge-gitops

Desired Kubernetes state for every environment. **Argo CD watches this repo; whatever is on `main` here is what runs in AKS.**

| Folder | Purpose |
|---|---|
| `helm/<service>/` | Helm chart per service (Phase 5) |
| `environments/<env>/` | Per-environment values: image tags, replicas, resources, URLs |
| `argocd/projects/` | AppProjects (RBAC boundaries for Argo CD) |
| `argocd/applications/` | Applications / ApplicationSets |

Write access:
- **DEV** image tags are committed directly by the Azure DevOps CI pipeline, using a write deploy key that is the only actor allowed to bypass PR rules.
- **QA / PROD** change only through reviewed pull requests (promotion = copying an already-tested tag).
- **Rollback** = `git revert` of the tag commit.
