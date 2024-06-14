---
description: >-
  Learn how to install the Kubernetes Dashboard Helm chart from a public
  repository.
---

# Install the Helm Chart

**Create a New Release**

When installing a Helm chart, a new release is created to manage the deployment. Here’s how to install the Kubernetes Dashboard:

```bash
helm install dashboard kubernetes-dashboard/kubernetes-dashboard -n monitoring --create-namespace
```

* **helm install**: Basic command to install a Helm chart.
* **dashboard**: Name of the Helm release created.
* **kubernetes-dashboard/kubernetes-dashboard**: Full name of the Helm chart, comprising the repository name (`kubernetes-dashboard`) and the chart name (`kubernetes-dashboard`).
* **-n monitoring** (or **--namespace monitoring**): Specifies the Kubernetes namespace where the release will be installed. If the namespace doesn't exist, it will be created.
* **--create-namespace**: Flag indicating that the specified namespace (`monitoring` in this case) should be created if it doesn't already exist.

<div align="right" data-full-width="false">

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption><p>The Helm install command</p></figcaption></figure>

</div>

**Verify Installation**

After installation, verify that the release was successful and obtain details about the deployment:

**1. List Helm Releases**

To list releases in a specific namespace (`monitoring`):

```bash
helm list --namespace monitoring
```

This command will show details about the `dashboard` release, including its revision, status, and chart version.

<div data-full-width="false">

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

</div>

**2. Get Details of the Helm Release**

To get detailed information about the Kubernetes objects managed by the release:

```bash
helm get all dashboard -n monitoring
```

This command displays comprehensive information about all Kubernetes resources created by the `dashboard` release in the `monitoring` namespace.

**3. Verify Kubernetes Objects**

Use `kubectl` commands to ensure that Kubernetes objects such as Pods, Deployments, and Services are correctly created:

*   **List Pods**:

    ```bash
    kubectl get pods -n monitoring
    ```
*   **List Deployments**:

    ```bash
    kubectl get deployment -n monitoring
    ```
*   **List Services**:

    ```bash
    kubectl get service -n monitoring
    ```
*   **Describe Deployment**:

    ```bash
    kubectl describe deployment dashboard-kubernetes-dashboard -n monitoring
    ```

    This command provides detailed information about the deployment, including labels, replicas, strategy type, and more.

By following these steps, you can effectively install the Kubernetes Dashboard using Helm, verify the installation, and ensure that all Kubernetes resources are correctly provisioned in your specified namespace (`monitoring`). Adjust namespace names and release names as necessary to fit your deployment environment and organizational requirements.
