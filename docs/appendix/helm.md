---
title:: Helm Introduction
---
# Helm

Helm is a package manager for Kubernetes based applications and resources deployment.

Helm also provides an easy way of accomplishing the following:

-   Install and uninstall kubernetes applications
-   Versioning complex kubernetes applications
-   Upgrade and rollback kubernetes applications

You can think of Helm as `yum` or `apt-get` package managers in Linux.

Helm has the following main components (not limited to):

-   Helm command line tool - provides interface to all Helm functionality
-   Charts - charts are manifests (yaml) files for desired kubernetes resources
-   Value file(s) - all customisable values for the application deployment can be configured here

!!!note
        Helm used to be a server-client application. Helm being the client and
        Tiller server component being installed in a kubernetes cluster. With
        Helm 3.x onwards, Tiller is removed and only Helm is used for ease.

##Installing Helm 3.x

Use the following commands to install helm in your LinuxTools VM.

```bash title="Install latest Helm through a script"
curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
chmod 700 get_helm.sh
./get_helm.sh
```
```bash title="Verify Helm version"
helm version
```
