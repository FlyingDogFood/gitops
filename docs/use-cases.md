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