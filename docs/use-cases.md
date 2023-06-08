# Use Cases
## App per project
```yaml
apps:
  app-a:
    groups:
      - environment/prod
    appTemplate: |
      {{ range $projectKey, $project := .Values.projects -}}
      ---
      apiVersion: argoproj.io/v1alpha1
      kind: Application
      metadata:
        name: {{ $project.name }}
        namespace: {{ .Release.Namespace }}
        labels:
          {{- include "gitops.labels" . | nindent 4 }}
        finalizers:
          - resources-finalizer.argocd.argoproj.io
      spec:
        project: {{ .Values.gitops.project }}
        
        sources:
          - repoURL: {{ .Values.project.repository }}
            targetRevision: {{ .Values.project.revision }}
            path: {{ .Values.project.path }}
      
        destination:
          server: https://kubernetes.default.svc
          namespace: {{ $project.name }}
            
        syncPolicy:
          {{- toYaml .Values.gitops.syncPolicy | nindent 4 }}
      {{ end -}}
```

## Use Versions for specific Components
You can every part of the gitops component by it's self.   
For example you can not version projects, groups and clusters.   
But use specific Versions for Apps.   
You would then set the revision for projects, groups and clusters to a branch(e.g. main).   
The revision for apps you would then set to a Versiontag.

## Specify specific Versions in groups or clusters
You can load specific revisions of components by setting the revision in you cluster or groups.   
Example for cluster:   
```
cluster: 
  name: cluster-a
  groups:
    - environment/prod

gitops:
  apps:
    revision: v0.1.9
```

Example for group:   
```
groups:
  environment/prod:
    projects:
    - project-a
    apps:
    - app-a
    
gitops:
  apps:
    revision: v0.1.9
```