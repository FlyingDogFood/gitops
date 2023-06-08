# Simple
In this example it's shown how to do a simple setup with the gitops chart. It does not use projects to reduce complexity.   
It deploys depending on the cluster 2 pods or in dev cluser 3 pods. The Image is set by the cloud group and the seeptime is set by the environment group.   
Notice: It is not recommendend to deploy pods with setup. You should rather deploy ArgoCD Apps that are deploying your own charts.

## Installation
```
helm install gitops gitops \
    --namespace <argocd-namespace> \
    --set cluster.name="<dev|stage|prod>"
    --set gitops.repository="https://github.com/FlyingDogFood/gitops.git" \
    --set gitops.revision="main" \
    --set gitops.apps.path="examples/simple/apps" \
    --set gitops.clusters.path="examples/simple/clusters" \
    --set gitops.groups.path="examples/simple/groups" \
```