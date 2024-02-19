---
description: Learn to set variables in Terraform using the command line.
---

# Setting a Variable on the Command Line

### Setting Variables via Command Line

You can set values for variables directly from the command line. Here's how:

**1. Set `bucket_suffix`:**

```bash
terraform apply -var bucket_suffix=hello
```

Terraform will prompt you for a value for `bucket_name` since it doesn't have a default. Once you provide a name, Terraform will create a bucket with the specified suffix (e.g., "hello").

**2. Set Both Variables:**

```bash
terraform apply -var bucket_name=kevholditch -var bucket_suffix=foo
```

With this command, you're setting values for both `bucket_name` and `bucket_suffix`. Terraform won't stop to ask for `bucket_name` since you've provided it on the command line.

📝 Note: When you're finished with your project, it's essential to run `terraform destroy` to delete all the resources. Confirm with "yes" to ensure the removal of these resources.

By using the `-var` flag followed by the variable name and the desired value, you can conveniently customize your Terraform project from the command line. This flexibility allows you to adapt your infrastructure configurations easily.
