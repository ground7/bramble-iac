<div align="center">

<img src="images/rpi4.png"/>

### **My Raspberry Pi Kubernetes Cluster** (Bramble :deciduous_tree:) <!-- omit in toc -->

_... created and managed by Flux_ (IaC :large_blue_diamond:) <!-- omit in toc -->

</div>

<br/>

<div align="center">

[![k3s](https://img.shields.io/badge/k3s-v1.20.10-brightgreen?style=for-the-badge&logo=kubernetes&logoColor=white)](https://k3s.io/)
[![pre-commit](https://img.shields.io/badge/pre--commit-enabled-brightgreen?logo=pre-commit&logoColor=white&style=for-the-badge)](https://github.com/pre-commit/pre-commit)
[![renovate](https://img.shields.io/badge/renovate-enabled-brightgreen?style=for-the-badge&logo=renovatebot&logoColor=white)](https://github.com/renovatebot/renovate)
[![Lines of code](https://img.shields.io/tokei/lines/github/ground7/bramble-iac?style=for-the-badge&color=brightgreen&label=lines&logo=codefactor&logoColor=white)](https://github.com/ground7/bramble-iac/graphs/contributors)

</div>

---

## :book:&nbsp; Overview <!-- omit in toc -->

- [:toolbox:&nbsp; Cluster Hardware](#toolbox-cluster-hardware)
- [:open_file_folder:&nbsp; Repository Structure](#open_file_folder-repository-structure)
- [:heavy_check_mark:&nbsp; Install Dependencies](#heavy_check_mark-install-dependencies)
- [:robot:&nbsp; Ansible Playbooks](#robot-ansible-playbooks)

### :toolbox:&nbsp; Cluster Hardware

&nbsp;|Name|Role|Storage
:-:|:-:|:-:|:-:
![elderberry](images/elderberry.png)|Elderberry|K3s Server Node 1|Flash
![cranberry](images/cranberry.png)|Cranberry|K3s Server Node 2|Flash
![snowberry](images/snowberry.png)|Snowberry|K3s Server Node 3|Flash
![strawberry](images/strawberry.png)|Strawberry|K3s Agent Node 1|Flash & SSD
![blueberry](images/blueberry.png)|Blueberry|K3s Agent Node 2|Flash & SSD
![blackberry](images/blackberry.png)|Blackberry|K3s Agent Node 3|Flash & SSD
![boysenberry](images/boysenberry.png)|Boysenberry|K3s Agent Node 4|Flash & SSD
![dingleberry](images/dingleberry.png)|Dingleberry|K3s Agent Node 5|Flash

![elderberry](images/elderberry.png)|![cranberry](images/cranberry.png)|![snowberry](images/snowberry.png)|![strawberry](images/strawberry.png)|![blueberry](images/blueberry.png)|![blackberry](images/blackberry.png)|![boysenberry](images/boysenberry.png)|![dingleberry](images/dingleberry.png)
:-:|:-:|:-:|:-:|:-:|:-:|:-:|:-:
Elderberry|Cranberry|Snowberry|Strawberry|Blueberry|Blackberry|Boysenberry|Dingleberry
Server 1|Server 2|Server 3|Agent 1|Agent 2|Agent 3|Agent 4|Agent 5
||||SSD|SSD|SSD|SSD||

### :open_file_folder:&nbsp; Repository Structure

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

### :heavy_check_mark:&nbsp; Install Dependencies

### :robot:&nbsp; Ansible Playbooks