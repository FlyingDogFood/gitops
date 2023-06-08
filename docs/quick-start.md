# Quick Start

Look at [prerequisites](prerequisites.md) before continuing.

## Installation
Clone gitops git Repository:
`git clone https://github.com/FlyingDogFood/gitops.git`
Switch to git repo:
`cd gitops`
Switch to wanted release or branch:
`git switch v0.0.1`
Install helm chart:
```bash
helm install gitops gitops \
    --namespace <argocd-namespace> \
    --set gitops.repository="https://github.com/FlyingDogFood/gitops.git" \
    --set gitops.revision="v0.0.1" \
    --set cluster.name="<cluster-name>"
```