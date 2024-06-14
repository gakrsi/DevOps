---
description: how to upgrade a version of a Helm release.
---

# Upgrade Helm Release

### Helm Upgrade Command Explained

The `helm upgrade` command in Helm is used to update an existing Helm release with new configurations or changes. Here’s a detailed explanation of how it works and its parameters:

**Basic Usage**

```bash
helm upgrade [RELEASE_NAME] [CHART] [flags]
```

* **`[RELEASE_NAME]`**: This is the name of the Helm release you want to upgrade.
* **`[CHART]`**: This specifies the chart you are upgrading, typically in the format `[repository]/[chartname]`.

**Parameters Explained**

* **`-n, --namespace`**: Specifies the Kubernetes namespace where the release is located. In your case, it's `-n monitoring`.
* **`--install`**: Ensures that if the release doesn't exist, Helm will install it. This flag is useful during upgrades when you're not sure if the release has been installed previously.
* **`--create-namespace`**: Creates the Kubernetes namespace if it doesn't already exist. This is helpful when deploying into a new namespace during upgrades.

**Example Command**

```bash
helm upgrade dashboard kubernetes-dashboard/kubernetes-dashboard -n monitoring --install --create-namespace --values dashboard.yaml
```

* **`dashboard`**: The name of the Helm release to upgrade.
* **`kubernetes-dashboard/kubernetes-dashboard`**: The chart repository and chart name.
* **`-n monitoring`**: The namespace where the release is deployed.
* **`--install`**: Ensures that Helm installs the release if it doesn't exist.
* **`--create-namespace`**: Creates the `monitoring` namespace if it's not already present.
* **`--values dashboard.yaml`**: Specifies a YAML file (`dashboard.yaml`) containing override values for the upgrade.

**Viewing Release Information**

After upgrading, you can check the status and history of the release:

* **`helm list -n monitoring`**: Lists all releases in the `monitoring` namespace.
* **`helm history dashboard -n monitoring`**: Shows the revision history of the `dashboard` release in the `monitoring` namespace. This helps track changes and rollbacks.

**Checking Overridden Values**

To see which values were applied during the upgrade, you can use:

```bash
helm get values dashboard -n monitoring
```

This command displays only the values that were explicitly overridden or set during the upgrade process. It's useful for debugging and verifying the configuration of your Helm release.

**Conclusion**

The `helm upgrade` command is essential for managing updates to Helm releases, allowing you to apply changes to existing deployments seamlessly. By understanding its parameters and using tools like `helm list`, `helm history`, and `helm get`, you gain insight into your deployments and ensure they meet your application's evolving requirements.
