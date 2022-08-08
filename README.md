[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://opensource.org/licenses/Apache-2.0)[![Go CI](https://github.com/camunda/camunda-platform-helm/actions/workflows/go.yml/badge.svg)](https://github.com/camunda/camunda-platform-helm/actions/workflows/go.yml)[![Artifact Hub](https://img.shields.io/endpoint?url=https://artifacthub.io/badge/repository/camunda)](https://artifacthub.io/packages/search?repo=camunda)

- [Camunda Platform Helm](#camunda-platform-helm)
  * [Installing Charts](#installing-charts)
  * [Configure Charts](#configure-charts)
  * [Uninstalling Charts](#uninstalling-charts)
  * [Deprecation of zeebe charts](#deprecation-of-zeebe-charts)
  * [Issues](#issues)
  * [Contributing](#contributing)

# Camunda Platform Helm
 
The Camunda Platform Helm repo, contains and host Camunda Platform related helm charts.

The charts can be accessed by adding the following Helm repo to your Helm setup:

```sh
helm repo add camunda https://helm.camunda.io
helm repo update
```

The charts are represented in the following image:
![HELM CHARTS](imgs/HelmChartImage.png)


## Installing Charts

You can install the Helm Charts by running:

```sh
helm install <YOUR HELM RELEASE NAME> camunda/camunda-platform
```

Per default the following will be installed:

- [camunda-platform](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md)
  - [Zeebe](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md#zeebe)
  - [Zeebe Gateway](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md#zeebe-gateway)
  - [Operate](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md#operate)
  - [Tasklist](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md#tasklist)
  - [Optimize](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md#optimize)
  - [Identity](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md#identity)
    - [Keycloak](https://github.com/bitnami/charts/tree/master/bitnami/keycloak)
    - [PostgreSQL](https://github.com/bitnami/charts/tree/master/bitnami/postgresql)
  - [ElasticSearch](https://github.com/elastic/helm-charts/tree/master/elasticsearch)

Follow [the instructions in the Camunda Platform documentation](https://docs.camunda.io/docs/self-managed/zeebe-deployment/kubernetes/index/) to install Camunda Platform to a K8s cluster.

> ***Note**: check the [kind/camunda-platform-core-kind-values](https://github.com/camunda/camunda-platform-helm/blob/main/kind/camunda-platform-core-kind-values.yaml) file to get camunda-platform running with kind*

## Configure Charts

Helm charts can be configured via using extra values files or directly via the `--set` option. make sure to check out the [Camunda Platform Helm Charts Readme](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md) for more information.

Example to enable the prometheus servicemonitor for Zeebe:

```sh
helm install <YOUR HELM RELEASE NAME> camunda/camunda-platform --set zeebe.prometheusServiceMonitor.enabled=true
```

## Uninstalling Charts

You can remove these charts by running:

```
helm uninstall <YOUR HELM RELEASE NAME>
```

> Notice that all the services and pods will be deleted, but not the Persistence Volume Claims which are used to hold the storage for the data generated by the cluster and Elasticsearch. In order to free up the storage you need to manually delete all the Persistent Volume Claims. You can do this by running:

```
kubectl get pvc
```

Then delete the ones that you don't want to keep:

```
kubectl delete pvc <PVC ids here>
```

Or delete the related kubernetes namespace, which contains the resources.

## Deprecation of zeebe charts

With the creation of the Camunda Platform Helm charts (previously known as ccsm-helm), the old zeebe-* charts have been deprecated.
This means they are no longer part of the repository and no longer maintained. The packaged charts are still available
for download.

The following charts are deprecated:

 * zeebe-full-helm
 * zeebe-cluster-helm
 * zeebe-operate-helm
 * zeebe-tasklist-helm

The new `camunda-platform` chart is a full replacement of `zeebe-full-helm` and replaces (contains) all other charts as sub-charts.
All sub-charts in `camunda-platform` are per default enabled.

For a complete migration guide see [here](https://github.com/camunda/camunda-platform-helm/blob/main/MIGRATION.md).

## Issues

Please create [new issues](https://github.com/camunda/camunda-platform-helm/issues) if you find problems with these charts. This repository is hosted using GitHub Pages and the source code repository can be found [here](https://github.com/camunda/camunda-platform-helm).

## Contributing

Please familiar yourself with the [contribution guide](https://github.com/camunda/camunda-platform-helm/blob/main/CONTRIBUTING.md) to find out how to contribute to this project. Please also make sure to check the [Camunda Platform Helm Charts Readme](https://github.com/camunda/camunda-platform-helm/blob/main/charts/camunda-platform/README.md) to find more information about configuring and developing the charts.
