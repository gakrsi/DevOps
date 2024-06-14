---
description: Get acquainted with the first Helm commands.
---

# Helm CLI

### Working with Helm CLI

Helm is primarily a command-line tool, offering extensive capabilities for managing Kubernetes applications. While some GUI tools exist, they may lack feature parity with Helm CLI.

**helm help Command and --help Flag**

* **helm help**: Displays environment variables for configuring Helm and lists all available commands.
* **helm \[command] --help**: Provides detailed usage information for a specific command, helping understand its parameters and options.

**helm version Command**

* **helm version**: Checks and displays the currently installed Helm version, ensuring compatibility and identifying the build information.

Example output: `version.BuildInfo{Version:"v3.11.0", GitCommit:"472c5736ab01133de504a826bd9ee12cbe4e7904", GitTreeState:"clean", GoVersion:"go1.18.10"}`

**helm env Command**

* **helm env**: Outputs configured environment variables for the Helm client, useful for debugging and configuration checks.

Example output:

```makefile
HELM_BIN=<YOUR_PATH_TO_HELM_BIN>
HELM_CACHE_HOME=<YOUR_PATH_TO_HELM_CACHE>
HELM_CONFIG_HOME=<YOUR_PATH_TO_HELM_CONFIG>
HELM_DATA_HOME=<YOUR_PATH_TO_HELM_CONFIG>
HELM_DEBUG="false"
HELM_KUBEAPISERVER=""
HELM_KUBEASGROUPS=""
HELM_KUBEASUSER=""
HELM_KUBECAFILE=""
HELM_KUBECONTEXT=""
HELM_KUBETOKEN=""
HELM_MAX_HISTORY="10"
HELM_NAMESPACE="monitoring"
HELM_PLUGINS=<YOUR_PATH_TO_HELM_PLUGINS>
HELM_REGISTRY_CONFIG=<YOUR_PATH_TO_HELM_CONFIG>
HELM_REPOSITORY_CACHE=<YOUR_PATH_TO_HELM_CACHE>
HELM_REPOSITORY_CONFIG=<YOUR_PATH_TO_HELM_CONFIG>
```

Understanding these commands is crucial for effectively using Helm CLI in Kubernetes environments, ensuring smooth application deployments and management.

### Common actions for Helm:

* helm search: search for charts
* helm pull: download a chart to your local directory to view
* helm install: upload the chart to Kubernetes
* helm list: list releases of charts
