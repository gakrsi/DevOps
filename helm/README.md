---
description: >-
  Welcome to a course on Helm, a crucial tool for building cloud solutions. If
  you're familiar with Kubernetes, understanding Helm is essential.
---

# Helm

<figure><img src="../.gitbook/assets/image.png" alt=""><figcaption><p>Helm Logo</p></figcaption></figure>

## Why Learn Helm?

**Importance for DevOps and Software Engineers:**

* Helm is essential for DevOps engineers and recommended for software engineers to understand its basics.
* A search for Helm on GitHub shows its widespread use, particularly in repositories for open-source software that run on Docker or Kubernetes.
* Many job descriptions for DevOps engineers require knowledge of both Kubernetes and Helm.

**Industry Recognition:**

* Helm is a graduated project by the CNCF, highlighting its importance and maturity for production use in cloud ecosystems.

## What Problem Does Helm Solve? <a href="#page-title" id="page-title"></a>

#### Introduction to Kubernetes

**Overview:**

* Kubernetes is a popular open-source container orchestration platform released by Google, based on its internal tool, Borg.
* It simplifies deploying and managing containerized applications in the cloud, such as those using Docker, by scaling them and ensuring their availability.
* Kubernetes abstracts server infrastructure management through objects defined in .yaml files.

**Key Concepts:**

**Pod:**

* The smallest and most basic Kubernetes object.
* Represents a running application, usually a single container (e.g., NGINX server).

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.21
    ports:
    - containerPort: 80
```

**Deployment:**

* Manages multiple instances of a Pod.
* Ensures a specified number of Pod replicas are running, automatically restarting any that fail.

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.21
        ports:
        - containerPort: 80
```

**Service:**

* Exposes applications to other software within or outside the Kubernetes cluster.
* Provides static addresses to Pods, ensuring consistent access even if Pods are recreated with different IP addresses.
* Example:

```yaml
apiVersion: v1
kind: Service
metadata:
  name: nginx
  labels:
    app: nginx
spec:
  type: NodePort
  ports:
    - name: http
      port: 80
      targetPort: 80
  selector:
    app: nginx
```

**Additional Kubernetes Objects:**

* **Ingress:** Manages external access to applications in a cluster.
* **Volumes:** Persist data by representing directories for files.
* **ConfigMap:** Stores and injects environment variables into Pods.
* **Secret:** Stores sensitive information like passwords securely.
* **Custom Resource:** Extends the Kubernetes API with new objects.

**Scaling and Complexity:**

* As applications grow, the number of Kubernetes objects and YAML files increases, making management complex.
* This complexity is even greater in distributed systems with many applications.

**Enter Helm:**

* Helm simplifies managing Kubernetes applications and their configurations.
* It helps scale and maintain multiple Kubernetes objects efficiently.

## What is Helm?

**Overview:**

* Helm is described on its official website [https://helm.sh](https://helm.sh) as "The package manager for Kubernetes."
* It helps find, share, and use software built for Kubernetes by bundling Kubernetes resource files into a single package called a chart.

**Comparison with Other Package Managers:**

* Similar to how `apt` (Linux), `winget` (Windows), `brew` (macOS), `npm` (JavaScript), `pip` (Python), and `maven` (Java) simplify software management, Helm simplifies managing Kubernetes applications.

**Helm Chart:**

* A package in Helm is called a chart.
* Example command to install a chart: `helm install elastic-operator eck-operator`
* Without Helm, installing complex applications like the Elastic Stack would be much more difficult and less secure.

**Purpose and Benefits:**

* Kubernetes orchestrates containers and abstracts infrastructure but can be complex for application management.
* Helm simplifies this by providing an application-level abstraction, making Kubernetes easier to use.

**Templates and Configuration:**

* Helm charts use templates written in the Helm template language, based on Go templates and Sprig functions.
* These templates allow customization of Kubernetes resources, with placeholders in double curly brackets `{{ }}` for dynamic values.
* Example Deployment definition with Helm template:

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 2
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:{{ .Values.container.image.version }}
        ports:
        - containerPort: 80
```

**Overriding Default Values:**

* Default values in a chart can be overridden using the `--set` flag or a `values.yaml` file.
* Example using `--set` flag:

```sh
helm install nginx-app ./nginx-chart --set container.image.version=1.20
```

* Example using `values.yaml`:

```yaml
# values.yaml file
container:
  image:
    version: '1.20'
```

* Command:

```sh
helm install nginx-app ./nginx-chart --values ./values.yaml
```

**Releases:**

* A Helm release is a version of all Kubernetes resources running together, created by a `helm install` or `helm upgrade` command.
* Helm tracks the history of releases, allowing easy rollbacks.

**Key Benefits of Helm:**

1. **Parameterized Kubernetes YAMLs:** Reusable blueprints for Kubernetes resource files.
2. **Simplified Application Installation:** Single-command installation.
3. **Easy Configuration:** High-level abstractions that simplify interaction without deep Kubernetes API knowledge.
4. **Revision History Tracking:** Easy rollbacks to previous states.

**Additional Advantages:**

* **Testing and Linting:** Ensures high-quality Kubernetes YAML files.
* **Pre-built Solutions:** Access to many ready-to-use Helm charts for popular open-source solutions on Artifact Hub.

**Conclusion:**

* Helm significantly reduces the complexity of managing Kubernetes applications, making it an invaluable tool for DevOps and software engineers.

#### Key Takeaways

1. **Helm Overview:**
   * Helm is the package manager for Kubernetes, simplifying the management and deployment of Kubernetes applications.
2. **Purpose of Helm:**
   * Bundles Kubernetes resource files into a single package called a chart.
   * Provides an application-level abstraction to reduce Kubernetes complexity.
3. **Comparison with Other Package Managers:**
   * Similar to `apt`, `winget`, `brew`, `npm`, `pip`, and `maven` in simplifying software management.
4. **Helm Chart:**
   * Packages in Helm are called charts.
   * Simplifies installing complex applications like the Elastic Stack with a single command.
5. **Templates and Customization:**
   * Helm charts use templates based on Go templates and Sprig functions.
   * Templates allow dynamic configuration using placeholders (e.g., `{{ .Values.container.image.version }}`).
6. **Overriding Default Values:**
   * Values can be overridden using the `--set` flag or a `values.yaml` file.
7. **Releases:**
   * A Helm release is a version of Kubernetes resources created by `helm install` or `helm upgrade`.
   * Helm tracks release history for easy rollbacks.
8. **Key Benefits:**
   * **Parameterized Kubernetes YAMLs:** Reusable templates for Kubernetes resource files.
   * **Simplified Installation:** Install applications with a single command.
   * **Easy Configuration:** High-level abstractions simplify usage.
   * **Revision History:** Easily roll back to previous states.
9. **Additional Advantages:**
   * **Testing and Linting:** Ensures high-quality Kubernetes YAML files.
   * **Pre-built Solutions:** Access many ready-to-use Helm charts on Artifact Hub.
10. **Conclusion:**
    * Helm significantly reduces the complexity of managing Kubernetes applications, making it essential for DevOps and software engineers.
