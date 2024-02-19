---
description: >-
  Learn how to import existing resources into Terraform using the terraform
  import command.
---

# Importing an Existing Infrastructure

<figure><img src="../../.gitbook/assets/image.png" alt="" width="188"><figcaption></figcaption></figure>

**What is the `terraform import` command?**

* `terraform import` is used to integrate existing resources into Terraform, allowing us to manage pre-existing infrastructure without altering the resources themselves.
* Particularly useful when dealing with environments that already have established resources, as not all scenarios involve starting from scratch with new deployments.
* Provides a solution for situations where an administrator manually created a resource outside Terraform, enabling its inclusion within Terraform's management scope.
* Ideally, after adopting Terraform, the goal is to create and manage all new resources through Terraform.
* While the current Terraform version doesn't automatically generate configuration for an imported resource, it adds the resource to the state. Users need to manually create a matching configuration before running `terraform import`.
* Writing a configuration for existing resources can offer insights into their creation process and highlight any deviations from best practices. Future versions of Terraform are expected to automate configuration generation.

**When to use the `terraform import` command?**

* Valuable when transitioning from manual resource deployment (GUI or scripts) to adopting Terraform for managing cloud resources.
* Organizations already using cloud resources may want to incorporate them into Terraform for consistent management.
* An experimental approach involves using `terraform state rm` to remove a resource from the state file, allowing re-importing with `terraform import`.
* In scenarios with existing infrastructure, like load-balanced virtual machines, three options are available:
  1. Delete and redeploy existing infrastructure (impractical in production).
  2. Create new infrastructure with Terraform, causing a temporary expense increase.
  3. Create Terraform configuration and use `terraform import` to bring existing deployments under Terraform management.

**Benefits of using the `terraform import` command**

* Enables integration of existing resources without the need for recreation, avoiding downtime issues.
* Facilitates managing the entire cloud environment through Infrastructure as Code (IaC), ensuring consistency and ease of maintenance.

**Key Takeaways**

* `terraform import` allows the inclusion of existing resources into Terraform management.
* The command itself doesn't auto-generate configuration; it requires manual configuration creation.
* Valuable for transitioning to Terraform from manual resource deployment methods.
* Experimental use with `terraform state rm` allows practicing the import command.
* Brings existing resources into Terraform without recreation, supporting IaC principles.
