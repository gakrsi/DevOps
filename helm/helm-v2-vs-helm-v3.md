---
description: Learn the differences between Helm v2 and v3.
---

# Helm v2 Vs Helm v3

**Helm Evolution:** Helm, like many software tools, evolves over time, sometimes introducing breaking changes to improve functionality. Helm v3 represents a significant redesign aimed at enhancing the overall product.

**Removal of Tiller:**

* **Helm v2:** Tiller acted as a server, interacting with the Kubernetes API on behalf of clients. It posed security risks due to required admin privileges and potential exposure to attacks.
* **Helm v3:** Tiller was removed. Release information is now stored as Kubernetes secrets, improving security.

**Change of Client Commands:**

* Several commands were renamed for consistency:
  * `delete` → `uninstall`
  * `fetch` → `pull`
  * `inspect` → `show`
* Some commands were removed:
  * `home`, `init`, `reset`, `serve`

**Improvement in Chart Update Strategy:**

* **Helm v2:** Used a two-way merge for updates, which could cause discrepancies when changes were made outside Helm.
* **Helm v3:** Introduced a three-way strategic merge patch, considering the current state, previous state, and new manifest for updates, reducing discrepancies.

**Requirements.yaml Moved to Chart.yaml:**

* **Helm v2:** Dependencies were specified in a separate `requirements.yaml` file.
* **Helm v3:** Dependencies can be included directly in `Chart.yaml`, simplifying management.

These updates make Helm v3 a more secure, consistent, and user-friendly tool compared to its predecessor.
