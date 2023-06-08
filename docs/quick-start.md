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
    --set gitops.revision="v0.0.1"
```

## Add you own Configurations
To add your own Configurations you need to create your own Repository that Contains your own Clusters, Groups, Apps and Projects.   
They also can be in different Repositories.   
For easy of setup we assume following Repo structure:   
```
|-apps
|-clusters
|-groups
|-projects
```
For more information about content of the folders look at [configuration](configuration.md).
Update Insatllation:   
```
```bash
helm upgrade gitops gitops \
    --namespace <argocd-namespace> \
    --set gitops.repository="https://github.com/FlyingDogFood/gitops.git" \
    --set gitops.revision="v0.0.1" \
    --set gitops.apps.repository="<your-repo>" \
    --set gitops.apps.revision="<your-repo-revision>" \
    --set gitops.clusters.repository="<your-repo>" \
    --set gitops.clusters.revision="<your-repo-revision>" \
    --set gitops.groups.repository="<your-repo>" \
    --set gitops.groups.revision="<your-repo-revision>" \
    --set gitops.projects.repository="<your-repo>" \
    --set gitops.projects.revision="<your-repo-revision>" \
    --set cluster.name="<cluster-name>"
```