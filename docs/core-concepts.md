# Core Concepts
This documentation dexscribes the core concepts of the gitops helm chart.

The gitops helm chart is based on ArgoCD multiple sources and Helm.
It uses the concept of value files to dynamicly loading specific values files for groups, projects and apps and deploy the specified configuration.

## Groups
In the gitops helm chart everything is controlled by groups.
You define in the cluster what groups this cluster is part of and the chart will load the files for the sepcified groups
