# :deciduous_tree::deciduous_tree::deciduous_tree:&nbsp; Bramble IaC <!-- omit in toc -->

A collection of raspberry pi 4s running k3s on top of Ubuntu. The entire configuration is done via this repository using flux.
## Overview <!-- omit in toc -->

- [:open_file_folder:&nbsp; Repository structure](#open_file_folder-repository-structure)

## :open_file_folder:&nbsp; Repository structure

These are the directories under `cluster` ordered by how Flux will apply them.

- **base** directory is the entrypoint to Flux and contains pointers to all the upstream helm chart repositories
- **crds** directory contains custom resource definitions (CRDs) that need to exist globally in the cluster before anything else exists
- **core** directory (depends on **crds**) is for important infrastructure applications (grouped by namespace) that should never be pruned by Flux
- **apps** directory (depends on **core**) is for common applications (grouped by namespace) that can be pruned by Flux if they are not tracked by Git anymore

```
cluster
├── apps
│   ├── default
│   ├── kube-system
│   ├── monitoring
│   ├── networking
│   └── system-upgrade
├── base
│   └── flux-system
├── core
│   ├── cert-manager
│   ├── longhorn-system
│   ├── metallb-system
│   ├── namespaces
│   └── system-upgrade
└── crds
    ├── cert-manager
    ├── kube-prometheus-stack
    └── traefik
```