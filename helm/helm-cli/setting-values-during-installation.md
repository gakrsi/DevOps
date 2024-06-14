---
description: >-
  Learn how to override Helm chart's default values and how to upgrade a version
  of a Helm release.
---

# Setting Values during Installation

#### Helm Chart Default Values and Overrides

In Helm, default values for a chart are defined in a `values.yaml` file. This file serves as the interface for configuring the Helm release. Here’s how you can work with default values and override them as needed:

**Default Values in `values.yaml`**

The `values.yaml` file contains default configurations for the Helm chart. For example, for the Kubernetes Dashboard Helm chart, part of `values.yaml` might look like this:

```yaml
# Default values for kubernetes-dashboard
image:
  repository: kubernetesui/dashboard
  tag: v2.4.0
replicaCount: 1
```

This snippet shows default settings for the Docker image repository (`kubernetesui/dashboard`), tag (`v2.4.0`), and the number of replicas (`1`).

**Finding Default Values**

* **Artifact Hub**: Many Helm charts are listed on Artifact Hub, where you can find the default `values.yaml` along with other chart details.
* **GitHub Repository**: If the chart is hosted on GitHub, you can explore its repository to find `values.yaml` and understand all configurable properties.

**Overriding Default Values**

**Method 1: Using a YAML File (`--values` or `-f` flag)**

1.  **Create a YAML File**: You can create a YAML file, e.g., `dashboard.yaml`, to specify overrides:

    ```yaml
    image:
      tag: v2.0.0
    ```
2.  **Install with Override**: Use the `--values` (or `-f`) flag to specify the YAML file containing overrides:

    ```bash
    helm install dashboard kubernetes-dashboard/kubernetes-dashboard -n monitoring --create-namespace --values dashboard.yaml
    ```

    This command installs the Kubernetes Dashboard chart, overriding the `image.tag` from `v2.4.0` to `v2.0.0`.

    * **Advantage**: Easily manage multiple overrides in a structured YAML file.
    * **Tip**: Use `-f` for a shorter flag.

**Method 2: Using `--set` Flag**

Alternatively, you can use the `--set` flag directly in the command:

```bash
helm install dashboard kubernetes-dashboard/kubernetes-dashboard -n monitoring --create-namespace --set image.tag=v2.0.0
```

* **Drawback**: Cumbersome for multiple overrides as each value requires a separate `--set` flag.

**Choosing Between `--values` and `--set`**

* **YAML File (`--values`)**:
  * Recommended for managing multiple overrides.
  * Organizes configuration in a clear, version-controlled manner (e.g., Git).
* **`--set` Flag**:
  * Suitable for quick, one-off overrides.
  * Useful in dynamic environments like CI/CD pipelines.

**Conclusion**

Using Helm's `values.yaml`, `--values`, and `--set` flags provides flexibility in configuring Helm releases. By understanding default values and how to override them, you can effectively manage deployments, whether for testing, production, or CI/CD pipelines. Choose the method that best fits your deployment needs and organizational practices to streamline your Helm chart management.
