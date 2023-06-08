# Core Concepts
This documentation dexscribes the core concepts of the gitops helm chart.

The gitops helm chart is based on ArgoCD multiple sources and Helm.
It uses the concept of value files to dynamicly loading specific values files for groups, projects and apps and deploy the specified configuration.

## Helm Chart Value files
This chart makes use of helm value files.   
The cluster file and the groups, apps and projects will be loaded into the chart using helm value files. 
This means you can set values in every file but you should respect the reserved values. See [configuration](configuration.yaml)

## Groups
In the gitops helm chart everything is controlled by groups.
You define in the cluster what groups this cluster is part of and the chart will load the files for the sepcified groups.
