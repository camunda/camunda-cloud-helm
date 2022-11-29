# Camunda Platform 8 Helm

[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)
[![Test - Unit](https://github.com/camunda/camunda-platform-helm/actions/workflows/test-unit.yml/badge.svg)](https://github.com/camunda/camunda-platform-helm/actions/workflows/test-unit.yml)
[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/camunda)](https://artifacthub.io/packages/search?repo=camunda)

- [Overview](#overview)
- [Documentation](#documentation)
- [Installing Charts](#installing-charts)
  - [Local Kubernetes](#local-kubernetes)
  - [OpenShift](#openshift)
- [Configure Charts](#configure-charts)
- [Guides](#guides)
- [Uninstalling Charts](#uninstalling-charts)
- [Deprecation of Zeebe charts](#deprecation-of-zeebe-charts)
- [Issues](#issues)
- [Contributing](#contributing)
- [Releasing the Charts](#releasing-the-charts)
- [License](#license)

## Overview

Camunda Platform 8 Self-Managed Helm charts repo.

The Camunda Platform components are represented in the following image:

<p align="center">
  <img
    alt="Camunda Platform 8 Self-Managed Helm charts architecture diagram"
    src="imgs/camunda-platform-8-self-managed-architecture-diagram-combined-ingress.png"
    width="80%"
  />
</p>

Per default the following components will be installed:

- [camunda-platform](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md)
  - [Zeebe](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md#zeebe)
  - [Zeebe Gateway](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md#zeebe-gateway)
  - [Operate](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md#operate)
  - [Tasklist](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md#tasklist)
  - [Optimize](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md#optimize)
  - [Identity](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md#identity)
    - [Keycloak](https://github.com/bitnami/charts/tree/master/bitnami/keycloak)
    - [PostgreSQL](https://github.com/bitnami/charts/tree/master/bitnami/postgresql)
  - [Elasticsearch](https://github.com/elastic/helm-charts/tree/master/elasticsearch)

## Documentation

This repo is mainly for Helm charts documentation. For full details, please visit the official
[Camunda Platform 8 Self-Managed docs](https://docs.camunda.io/docs/self-managed/about-self-managed/).

## Installing Charts

The charts can be accessed by adding the Camunda Helm repo:

```sh
helm repo add camunda https://helm.camunda.io
helm repo update
```

Then, you can install the Helm charts by running:

```sh
helm install YOUR_RELEASE_NAME camunda/camunda-platform
```

> **Note**
> For more details about deploying Camunda Platform 8 on Kubernetes, please visit the
> [Helm/Kubernetes installation instructions docs](https://docs.camunda.io/docs/self-managed/platform-deployment/helm-kubernetes/overview/).

### Local Kubernetes

We recommend using Helm on KIND for local environments, as the Helm configurations are battle-tested
and much closer to production systems.

For more details, follow the Camunda Platform 8
[local Kubernetes cluster guide](https://docs.camunda.io/docs/self-managed/platform-deployment/helm-kubernetes/guides/local-kubernetes-cluster/).

### OpenShift

Check out [OpenShift Support](/openshift) to get started with deploying the charts on Red Hat OpenShift. 

## Configure Charts

Helm charts can be configured by using extra `values.yaml` files or directly via the `--set` option.
For more details, check out the [Camunda Platform 8 Helm Charts](./charts/camunda-platform/README.md).

## Guides

<!-- TODO: add a direct link for the guides section when we have it -->
Default values cannot cover every use case, for that reason, we have
[Camunda Platform 8 deploy guides](https://docs.camunda.io/docs/next/self-managed/platform-deployment/helm-kubernetes/overview/).
The guides have detailed examples for different use cases like Ingress setup and so on.

## Uninstalling Charts

You can remove these charts by running:

```sh
helm uninstall YOUR_RELEASE_NAME
```

> **Note**
>
> Notice that all the Services and Pods will be deleted, but not the PersistentVolumeClaims (PVC)
> which are used to hold the storage for the data generated by the cluster and Elasticsearch.

To free up the storage you need to manually delete all the PVCs.

First, view the PVCs:

```sh
kubectl get pvc -l app.kubernetes.io/instance=YOUR_RELEASE_NAME
kubectl get pvc -l release=YOUR_RELEASE_NAME
```

Then delete the ones that you don't want to keep:

```sh
kubectl delete pvc -l app.kubernetes.io/instance=YOUR_RELEASE_NAME
kubectl delete pvc -l release=YOUR_RELEASE_NAME
```

Or you can simply delete the related Kubernetes namespace, which contains all PVCs.

## Deprecation of Zeebe charts

With the creation of the Camunda Platform 8 Helm charts (previously known as `ccsm-helm`), the old `zeebe-*` charts
have been deprecated. This means they are no longer part of the repository and are no longer maintained.
However, the packaged charts are still available for download. But will be removed in the next releases.

The following charts are deprecated:
- zeebe-full-helm
- zeebe-cluster-helm
- zeebe-operate-helm
- zeebe-tasklist-helm

The new `camunda-platform` chart is a full replacement of `zeebe-full-helm` and replaces (contains) all other charts
as sub-charts. All sub-charts in `camunda-platform` are enabled by default.

For a complete migration guide, visit [migration docs](./MIGRATION.md).

## Issues

Please create a [new issue](https://github.com/camunda/camunda-platform-helm/issues) if you find any problem
in the Camunda Platform 8 Helm charts.

## Contributing

To start contributing to this project, please familiarize yourself with the
[contribution guide](https://github.com/camunda/camunda-platform-helm/blob/main/CONTRIBUTING.md).
Also, make sure to check the [Camunda Platform Helm Charts Readme](./charts/camunda-platform/README.md)
to find more information about configuring and developing the charts.

## Releasing the Charts

To find out how to release the charts please visit the [release guide](./RELEASE.md).

## License

Camunda Platform 8 Self-Managed Helm charts are licensed under the open-source Apache License 2.0.
Please see [LICENSE](LICENSE) for details.

For Camunda Platform 8 components, please visit
[licensing information page](https://docs.camunda.io/docs/reference/licenses).
