---
layout: docwithnav-pe
assignees:
- ashvayka
title: Thingsboard cluster installation using Helm
description: Install Kubernetes cluster with Helm for ThingsBoard IoT platform

---

{% assign docsPrefix = "pe/" %}

* TOC
{:toc}

This guide will help you to set up ThingsBoard cluster using Helm.

## Prerequisites

{% include templates/install/helm/helm-prerequisites.md %}

## Introduction

{% include templates/install/helm/helm-introduction.md %}

## Installing

{% include templates/install/helm/helm-installing.md %}

## Uninstalling

{% include templates/install/helm/helm-uninstalling.md %}

## Thingsboard services parameters

{% include templates/install/helm/helm-parameters.md %}

## Third-party services parameters

All configurations with *external* prefix need to be set if you already have this services configured.

All third party parameters that assigned it this chart are just a basics configurations and can be
modified with right prefix.

### Cache

{% include templates/install/helm/thirdparty/helm-internal-redis-parameters.md %}

{% include templates/install/helm/thirdparty/helm-internal-redis-cluster-parameters.md %}

{% include templates/install/helm/thirdparty/helm-external-redis-parameters.md %}

### Queue

{% include templates/install/helm/thirdparty/helm-internal-kafka-parameters.md %}

{% include templates/install/helm/thirdparty/helm-external-kafka-parameters.md %}

### Service Coordinator

{% include templates/install/helm/thirdparty/helm-internal-zookeeper-parameters.md %}

{% include templates/install/helm/thirdparty/helm-external-zookeeper-parameters.md %}

### PostgreSql parameters

{% include templates/install/helm/thirdparty/helm-internal-postgresql-parameters.md %}

{% include templates/install/helm/thirdparty/helm-external-postgresql-parameters.md %}

### Cassandra parameters

{% include templates/install/helm/thirdparty/helm-internal-cassandra-parameters.md %}

{% include templates/install/helm/thirdparty/helm-external-cassandra-parameters.md %}

### Service Providers parameters

{% include templates/install/helm/ingress/helm-aws-ingress.md %}

{% include templates/install/helm/ingress/helm-aks-ingress.md %}

{% include templates/install/helm/ingress/helm-gke-ingress.md %}

### Examples

### EKS
{% include templates/install/helm/examples/helm-aks-cluster-example.md %}

## Next steps

{% assign currentGuide = "InstallationGuides" %}{% include templates/guides-banner.md %}
