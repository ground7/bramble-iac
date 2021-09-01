<div align="center">

<p align="middle">
  <img src="/images/elderberry.png" width="32px" height="32px"/>
  <img src="/images/cranberry.png" width="32px" height="32px"/>
  <img src="/images/snowberry.png" width="32px" height="32px"/>
  <img src="/images/strawberry.png" width="32px" height="32px"/>
  <img src="/images/blueberry.png" width="32px" height="32px"/>
  <img src="/images/blackberry.png" width="32px" height="32px"/>
  <img src="/images/boysenberry.png" width="32px" height="32px"/>
  <img src="/images/dingleberry.png" width="32px" height="32px"/>
</p>


### My Raspberry Pi Kubernetes Cluster (Bramble :deciduous_tree:) <!-- omit in toc -->

_... created and managed by Flux (IaC :large_blue_diamond:)_

</div>

<br/>

<div align="center">

[![k3s](https://img.shields.io/badge/k3s-v1.20.10-brightgreen?style=for-the-badge&logo=kubernetes&logoColor=white)](https://k3s.io/)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white&style=for-the-badge)](https://github.com/pre-commit/pre-commit)
[![renovate](https://img.shields.io/badge/renovate-enabled-brightgreen?style=for-the-badge&logo=renovatebot&logoColor=white)](https://github.com/renovatebot/renovate)
[![Lines of code](https://img.shields.io/tokei/lines/github/ground7/bramble-iac?style=for-the-badge&color=brightgreen&label=lines&logo=codefactor&logoColor=white)](https://github.com/ground7/bramble-iac/graphs/contributors)

</div>

---

# :book:&nbsp; Overview <!-- omit in toc -->

- [:open_file_folder:&nbsp; Repository structure](#open_file_folder-repository-structure)

# :open_file_folder:&nbsp; Repository structure

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