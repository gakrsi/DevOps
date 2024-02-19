---
description: Learn how to use the show subcommand in Terraform.
---

# Viewing Resource Attributes in Terraform State

**The "terraform state show" Subcommand:**

The "terraform state show" command serves the purpose of displaying the attributes of a specific resource within the Terraform state.

**Syntax:** The syntax for the "show" subcommand is as follows: `terraform state show [options] ADDRESS`.

**Arguments:** The ADDRESS specified in the "show" subcommand must point to an instance of a resource and should not represent a grouping of resources created by count or for\_each. The attributes of the resource are presented in alphabetical order and are sent to stdout, typically for consumption by a parsing engine.

**Using the terraform state show Command:** This command is commonly utilized to inspect the values stored in particular attributes of a resource. The output can be employed by a subsequent process for post-configuration tasks on an instance or can be fed into a configuration management database (CMDB).

**Applying the terraform state show Command:** Suppose we want to examine the properties of our `aws_s3_bucket` resource. We can use the following command to view the attributes of the resource in the Terraform state:

```bash
terraform state show aws_s3_bucket.terraform_test_bucket_edu
```

It's important to note that the specified ADDRESS should represent a single instance of a resource. Also, the attributes are displayed in alphabetical order for ease of reference.

**Key Takeaways:**

* The "terraform state show" command is designed for displaying the attributes of a specific resource in the Terraform state.
* The syntax involves specifying the resource instance's ADDRESS.
* This command is useful for inspecting attribute values and is often used in conjunction with post-configuration processes or to feed information into a configuration management database (CMDB).
* Other commands like `mv`, `rm`, and `push` directly edit the existing state file, but caution is advised when using them. On the other hand, commands like `list`, `pull`, and `show` are primarily for viewing the state file contents in various formats.
