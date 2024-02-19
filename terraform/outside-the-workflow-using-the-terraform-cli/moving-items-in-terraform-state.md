---
description: Learn how to move items in a Terraform state.
---

# Moving Items in Terraform State

**What is the `terraform state mv` Command?**

The `terraform state mv` command in Terraform is your go-to tool when you need to relocate things within your Terraform state. It's like rearranging furniture in your digital house.

**Command Syntax:**

The syntax for this command goes like this: `terraform state mv [options] SOURCE DESTINATION`.

**Command Arguments:**

Now, let's break down the essential bits:

* The `dry-run` flag is like a preview mode, showing you what changes will happen without actually making them.
* The `state` flag points to the source state file, and if you're not using the default `terraform.tfstate` file or a remote backend, you need to specify it.
* The `state-out` flag indicates the destination file path. If not specified, Terraform uses the source state file.

**Using the `terraform state mv` Command:**

Why would you want to use this command? Here are a couple of scenarios:

1. **Resource Renaming:**
   * If you need to change the name of an existing resource without destroying and recreating it, you can update the name in your configuration and then use `terraform state mv` to match the changes.
   * For example, changing the name from `aws_instance.nginx` to `aws_instance.web`.
2. **Organizing Resources:**
   * You might want to move resources to a module or restructure your configuration without the hassle of destroying and recreating everything.
   * It's handy when replacing existing resource definitions with a module.
3. **Configuration Cleanup:**
   * When your configuration becomes too large, and you want to break it into smaller, more manageable parts, `terraform state mv` helps you move a bunch of resources to a new state file.

**How to Apply the `terraform state mv` Command:**

Let's walk through a quick example. Suppose you want to change the name label for a resource instance. First, update your code:

```hcl
resource "aws_instance" "nginx" {
  # ... other configurations
}
```

Change it to:

```hcl
resource "aws_instance" "web" {
  # ... other configurations
}
```

Now, run the `terraform state mv` command:

```bash
terraform state mv aws_instance.nginx aws_instance.web
```

This moves the resource from `aws_instance.nginx` to `aws_instance.web`. Simple, right?

**Key Takeaways:**

The `terraform state mv` command is your friend when you want to shuffle things around in your Terraform state without causing chaos. It's like rearranging your digital workspace – easy, organized, and no heavy lifting.
