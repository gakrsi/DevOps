---
description: Learn how to use the rm subcommand in Terraform.
---

# Removing Items from Terraform State

**The "terraform state rm" Subcommand:**

The "terraform state rm" command is used to eliminate elements from the Terraform state.

**Syntax:** The syntax for the "rm" subcommand is as follows: `terraform state rm [options] ADDRESS`.

**Using the terraform state rm Command:** This command is versatile, allowing the removal of a single resource, a specific instance of a resource, entire modules, and more. Crucially, resources removed using this command are deleted from the state file but remain unaffected in the actual target environment.

The most common application of the "rm" command is to withdraw a resource from Terraform management. This could happen if the resource is shifted to another configuration and imported, or if Terraform is being replaced by another tool. The primary objective is to eliminate the reference to the resource without actually destroying it.

**Applying the terraform state rm Command:** Suppose we decide to stop managing an `aws_s3_bucket` with Terraform. First, we execute the following command:

```bash
terraform state rm aws_s3_bucket.terraform_test_bucket_edu
```

This removes the specified resource from the Terraform state. Subsequently, we use the command:

```bash
terraform state list
```

To view the list of Terraform resources and decide which resource item we want to delete. Then, to remove a specific resource from the Terraform state, we run:

```bash
terraform state rm aws_s3_bucket.terraform_test_bucket_edu
```

It's important to note that removing a resource from the state file doesn't automatically remove it from the configuration. All references to the resource should be removed from the configuration before executing another `terraform plan` or `terraform apply`. Failure to do so might lead Terraform to attempt recreating the resource or result in errors due to invalid references.

**Key Takeaways:**

* Terraform state commands are designed for examining and manipulating the state content.
* The "terraform state rm" command is powerful for selectively removing resources from the Terraform state without affecting the actual resources in the target environment.
* Caution should be exercised to update the configuration and remove all references to the resource before running subsequent Terraform commands to avoid unintended recreations or errors.
