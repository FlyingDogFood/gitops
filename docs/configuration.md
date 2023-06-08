# Configuration
In Addition to the default values the ArgoCD App of the gitops chart will read more value files.  
The default values are discribed under [Helm Values](#Helm-Values).
The additional values files are discribed under:

- [Cluster](#Cluster)
- [Group](#Group)
- [Project](#Project)
- [App](#App)

## Helm Values
Value | Description | Type | Default | Example
---|---|---|---|---
`gitops.repository` | URL to the git reposiotry containing the gitops helm chart | string | | `https://github.com/FlyingDogFood/gitops.git`
`gitops.revision` | Git Revision for the gitops helm chart | string | | `main`
`gitops.path` | Path to the gitops chart in repository | string | `gitops` | `gitops`
`gitops.project` | ArgoCD project for the gitops app | string | `default` | `default`
`gitops.syncPolicy` | ArgoCD SyncPolicy for the gitops app | object | `TODO` | `TODO`
`gitops.clusters.path` | Path to the clusters folder | string | `clusters` | `clusters`
`gitops.clusters.repository` | Repository that hold the cluster value files | string | `https://github.com/FlyingDogFood/gitops.git` | `gitops.repository`
`gitops.clusters.revision` | Revision to the clusters folder | string | `main` | `gitops.revision`
`gitops.groups.path` | Path to the groups folder | string | `clusters` | `clusters`
`gitops.groups.repository` | Repository that hold the groups value files | string | `https://github.com/FlyingDogFood/gitops.git` | `gitops.repository`
`gitops.groups.revision` | Revision to the groups folder | string | `main` | `gitops.revision`
`gitops.projects.path` | Path to the projects folder | string | `clusters` | `clusters`
`gitops.projects.repository` | Repository that hold the projects value files | string | `https://github.com/FlyingDogFood/gitops.git` | `gitops.repository`
`gitops.projects.revision` | Revision to the projects folder | string | `main` | `gitops.revision`
`gitops.apps.path` | Path to the apps folder | string | `clusters` | `clusters`
`gitops.apps.repository` | Repository that hold the apps value files | string | `https://github.com/FlyingDogFood/gitops.git` | `gitops.repository`
`gitops.apps.revision` | Revision to the apps folder | string | `main` | `gitops.revision`
`cluster.name` | Name of the cluster, also sets the right cluster values file | string | | `cluster-a`
`cluster.groups` | Groups of the cluster, should be set over the cluster value file | []string | | `TODO`
`groups` | Map of the groups, build from group value files | map[string]group | | `TODO`
`projects` | Map of the projects, build from project value files | map[string]project | | `TODO`
`apps` | Map of the apps, build from app value files | map[string]app | | `TODO`

## Cluster
A Cluster value file discribes a cluster and contains of follwoing values.   
Please consider that the name of the value file has to be the same as `cluster.name`.    
Value | Description | Type | Default | Example
---|---|---|---|---
`cluster.name` | Name of the cluster | string | | `cluster-a`
`cluster.groups` | Groups of the cluster, will be used to load group values. The order will determinante the prioriority of groups, the last has the highest priority | []string | | `TODO`
`*` | Values can be used for free use to set values for a specific cluster | map[string]interface{} | | `TODO`   
Example:
cluster-a.yaml
```
cluster: 
  name: cluster-a
  groups:
    - environment/prod
    - cloud/aws
```

## Group
A Group value file discribes a values for a specific group.
Please consider that the name of the value file has to be the same as `groupName`.    
Value | Description | Type | Default | Example
---|---|---|---|---
`groups.<groupName>.projects` | Names of projects to deploy on the cluster, will be used to load project values | []string | | `TODO`
`groups.<groupName>.apps` | Names of apps to deploy on the cluster, will be used to load app values | []string | | `TODO`
`*` | Values can be used for free use to set values for a specific group | map[string]interface{} | | `TODO`
Example:
environment/prod.yaml
```
groups:
  environment/prod:
    projects:
    - project-a
    apps:
    - app-a
```

## Project
A Project value file describes values for a specific project, the exact implementation is left to the user.   
Please consider that the name of the value file has to be the same as `projectName`.    
Value | Description | Type | Default | Example
---|---|---|---|---
`projects.<projectName>.groups` | Names of groups to deploy the project to, can be used to automaticly write the name of project to group | []string | | `TODO`
`projects.<projectName>.*` | Values can be used for free use to set values for a specific project | map[string]interface{} | | `TODO`
Example:
project-a.yaml
```
projects:
  project-a:
    groups:
      - environment/prod
    name: project-a
```

## App
A App value file defines a specific app to deploy.   
Please consider that the name of the value file has to be the same as `appName`.    
Value | Description | Type | Default | Example
---|---|---|---|---
`apps.<appName>.groups` | Names of groups to deploy the app to, can be used to automaticly write the name of project to group | []string | | `TODO`
`apps.<appName>.appTemplate` | A template for a kubernetes object e.g. ArgoCD App. you can use helm values and functions e.g. `.Values` | string | | `TODO`
`apps.<appName>.*` | Values can be used for free use to set values for a specific app | map[string]interface{} | | `TODO`
Example:
app-a.yaml
```
apps:
  app-a:
    groups:
      - environment/prod
    appTemplate: |
      apiVersion: v1
      kind: Pod
      metadata:
        name: app-a
      spec:
        containers:
          - command:
              - sleep
              - "3600"
            image: redhat/ubi8
            name: app-a
```