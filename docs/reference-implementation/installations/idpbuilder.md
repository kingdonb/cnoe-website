---
sidebar_position: 0
description: IDP builder is a single binary IDP launcher.
title: idpBuilder CLI
---

:::note github repo

[cnoe-io/idpbuilder](https://github.com/cnoe-io/idpbuilder)
:::

Spin up a complete internal developer platform using industry standard technologies like Kubernetes, Argo, and backstage with only Docker required as a dependency.

This is also a completely self-contained binary, meaning you can get up and running simply by downloading a binary release and executing it!

## IDP installation flow

The idpbuilder cli installs a local internal developer portal using the following pattern

1. Create a new Kind cluster if one doesnt exist or if `--recreate` switch is passed.
1. Create a gitserver docker image with the embeded argocd application resources.
1. Create a new gitserver pod, service and ingress serving the argocd applications via the git protcol.
1. Install ArgoCD and configure it to be able to monitor the gitserver service.
1. Install Argo Project and Argo applications for the embeded Argo apps.
1. Argo apps are reconciled by ArgoCD.
1. Command line exits leaving the cluster running with the IDP install.
1. Backstage will become available on your localhost via an nginx ingress. Use kubectl to get the correct IDP address/hostname to connect to.

## Installation

- Docker must be installed and available to the current user.
- Internal Developer Portal components are installed as ArgoCD Applications.
- The ArgoCD apps that are installed are embedded in the cli binary. See [cnoe-io/idpbuilder/pkg/controllers/localbuild/controller.go](https://github.com/cnoe-io/idpbuilder/blob/56089e4ae3b27cf90641bfbff2a96c36dd5263e1/pkg/controllers/localbuild/controller.go#L211-L243)
