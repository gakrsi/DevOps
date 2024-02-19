---
description: Learn how to taint a resource in the state using terraform taint command.
---

# Taint command

**What is the `terraform taint` command?**

* The `terraform taint` command marks a resource in the Terraform state as tainted. This implies that the resource will be destroyed and recreated during the next application of the configuration.
* Executing `terraform taint` doesn't instantly destroy the resource but edits the state. The actual destruction and recreation happen when you run `terraform apply` after tainting.

**Syntax:**

* The command follows the syntax `terraform taint [options] <address>`, where `<address>` is the resource's address in the configuration.

**Example:**

* If we have an AWS S3 bucket named `terraform_test_bucket_edu`, running `terraform taint aws_s3_bucket.terraform_test_bucket_edu` marks it as tainted.
* Viewing the state file with `terraform show` would indicate the taint status of the resource.

**When to use `terraform taint`?**

* It's useful when a change isn't apparent to Terraform, or the internal state of a resource is known to be problematic.
* For instance, changes to a virtual machine's startup script may not be detected by Terraform. Tainting signals Terraform to recreate the resource, ensuring changes take effect.
* Resources dependent on the tainted resource may also undergo modifications to remain consistent.

**Applying the `terraform taint` command:**

* When changes in code lead to a failed plan during `terraform apply`, tainting signals that a resource is incorrect.
* Running `terraform plan` after tainting indicates which resources will be destroyed and recreated.
* It's possible to remove the taint using `terraform untaint`, helpful for accidental taints or clearing taints applied by Terraform on a failed resource provisioning.

**Key Takeaways:**

* `terraform taint` marks resources for destruction and recreation when Terraform may not automatically recognize invalid or incorrectly configured resources.
