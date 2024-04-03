---
description: Learn how to delete an infrastructure managed by Terraform.
---

# Destroy Terraform-managed Infrastructure

### Purpose of the `terraform destroy` command <a href="#purpose-of-the-terraform-destroy-command" id="purpose-of-the-terraform-destroy-command"></a>

Destroying what we deployed seems counterintuitive, but there are many cases where it might be useful. We might be deploying development environments for a project and want to clean up the resources when the project concludes. We might be building an environment for testing in a CI/CD pipeline and want to tear down the environment when the tests are complete. The `terraform destroy` command is used to destroy Terraform-managed infrastructure.

The `terraform destroy` command is a powerful command. It deletes all resources under management by Terraform. This action can’t be undone. For that reason, Terraform presents an execution plan for all resources that’ll be destroyed and prompts us to confirm before performing the destroy operation.

### Arguments <a href="#arguments" id="arguments"></a>

In many respects, the `terraform destroy` command is a mirror of the `terraform apply` command, except that we can’t give it an execution plan. This command accepts all arguments and flags that the `terraform apply` command accepts, with the exception of a plan file argument. We can preview what the command will do by running `terraform plan -destroy` along with any other necessary arguments. We can’t save the execution plan to a file and submit it to the `terraform destroy` command.

There are two arguments that are useful to know:

* `-auto-approve` won’t prompt the user for confirmation and used to be called `-force`, which has been deprecated.
* `-target` lets us specify a target, and only the target and its dependencies will be destroyed. This flag can be used multiple times.

### Key takeaways <a href="#key-takeaways" id="key-takeaways"></a>

The `terraform destroy` command permanently deletes all resources managed by the current configuration and state. The command will prompt for confirmation, and select resources can be targeted with the `-target` argument.
