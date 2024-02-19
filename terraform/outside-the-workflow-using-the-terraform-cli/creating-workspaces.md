---
description: Learn when and how to create a workspace in Terraform.
---

# Creating Workspaces

**What is a Workspace in Terraform?**

* In Terraform, a workspace refers to independently managed state files within the context of Terraform Cloud or Terraform open-source.
* Focusing on Terraform open-source, workspaces are configurations that share a common configuration but have their own state files.
* Previously, the concept of an environment was managed with the `terraform env` command. However, it's now an alias for `terraform workspace` and may be deprecated in the future.

**Workspace for Multiple Environments:**

* Organizations often have various environments like development, testing, staging, and production. Each Terraform workspace represents the deployment of a configuration in one of these environments.
* Using a single configuration across multiple environments ensures consistency as applications progress from development to production.
* HashiCorp suggests organizing configurations to represent separate architecture components within an environment for better clarity and management.

**How does a Workspace work?**

* Each workspace has persistent data, usually stored as a state file in the backend. Terraform starts with a default workspace that cannot be deleted, and additional workspaces can be created, selected, and deleted.
* The backend, where Terraform state is stored, may vary, and not all backends support the use of workspaces. Some examples include local file backend and Amazon S3.

**Terraform Workspace Commands:**

* Workspaces are managed through `terraform workspace` commands, including:
  * `new`: Creates and selects a new workspace.
  * `select`: Chooses an existing workspace.
  * `list`: Lists existing workspaces.
  * `show`: Displays the name of the current workspace.
  * `delete`: Removes an empty workspace (requires it to be unselected, and state file must be empty).
* When using `terraform workspace delete`, the `-force` flag can be specified if the state file isn't empty, abandoning resources created by the state file.

**Creating a Workspace in Terraform:**

* To create a new workspace, run `terraform workspace new development` in the terminal.
* If the workspace already exists, use `terraform workspace new <workspace name>` to create another.
* In a local file backend, Terraform creates folders for each workspace in the `terraform.state.d` directory.
* Running `terraform plan` generates a plan within the current workspace context. Resources created in other workspaces exist but are not part of the state for the current workspace. Differentiating resources is crucial to avoid collisions between workspaces.

**Key Takeaways:**

* Terraform workspaces combine state files and configurations for managing instances of a configuration in various environments.
* The default workspace cannot be deleted.
* Proper organization and differentiation of resources are essential when using multiple workspaces.
