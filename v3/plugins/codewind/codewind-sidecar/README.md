# Codewind on Eclipse Che

**Note:** This plugin **must** be installed alongside `codewind-theia`.

## Setting up the roles

The Codewind plugins rely on additional roles than what Che workspaces are given by default. Prior to starting your workspace with the `codewind-theia` and `codewind-sidecar` plugins, run the following commands:
- `kubectl apply -f https://raw.githubusercontent.com/eclipse/codewind-che-plugin/0.8.0/setup/install_che/codewind-clusterrole.yaml` to create the Codewind clusterrole
- `kubectl apply -f https://raw.githubusercontent.com/eclipse/codewind-che-plugin/0.8.0/setup/install_che/codewind-rolebinding.yaml -n <namespace>`, where `<namespace>` is the namespace where your Che workspace will be running, to create the corresponding RoleBinding for the Che workspace service account.

## Allowing Root and Privileged Containers

Codewind currently uses `Buildah` to build container images. As a result, Codewind currently needs to run as root and privileged. If you're running Codewind on OpenShift, run the following commands to enable that:
- To enable root containers: `oc adm policy add-scc-to-user anyuid system:serviceaccount:<namespace>:che-workspace`, where `<namespace>` is the namespace where your Che workspace will be running.
- To enable privileged containers: `oc adm policy add-scc-to-user anyuid system:serviceaccount:privileged:che-workspace`, where `<namespace>` is the namespace where your Che workspace will be running.

## Installing Codewind

1. Install both the `codewind-theia` and `codewind-sidecar` plugins into your Che workspace.
2. Start (or restart) your Che workspace. 