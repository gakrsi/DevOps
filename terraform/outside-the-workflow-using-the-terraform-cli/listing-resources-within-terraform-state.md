---
description: Learn how to list resources within a Terraform state.
---

# Listing Resources within Terraform State

**What is a State in Terraform?**

In Terraform, the state is like a record-keeper that holds crucial information about your infrastructure. It's a JSON document stored locally or on a remote server, helping Terraform keep track of what resources are created and how they're configured. It's like a blueprint for your infrastructure.

Now, here's the catch – you're strongly advised not to mess with this state file directly. However, there are moments when you might need to peek into it or make some tweaks. In those cases, Terraform provides the `terraform state` command and a bunch of helpful subcommands.

**Terraform State Subcommands:**

Here's a quick rundown of some of the `terraform state` subcommands you might find handy:

* `list`: Shows you a list of resources in the state.
* `mv`: Moves an item around in the state.
* `pull`: Grabs the current state and displays it.
* `push`: Updates the remote state based on a local state file.
* `rm`: Removes instances from the state.
* `show`: Displays details about a specific resource in the state.

**Resource Addressing:**

Now, when you use the `terraform state` command, you'll often want to focus on specific resource instances in the state. Terraform uses what they call standard address syntax, which is basically how we refer to resources in our configuration file.

It looks like this: `[module path][resource spec]`. The `resource spec` part is the path to the instance in a given module. For example, if you have a subnet in an Azure vnet module, it could be something like `module.my-vnet.azurerm_subnets.subnet[0]`.

**Using the `terraform state list` Command:**

Now, imagine you've deployed an AWS instance in the default VPC, and you want to see a list of all the resources created by your configuration. You'd use the `terraform state list` command like this:

```bash
# To show a list of resources
terraform state list
```

This command gives you a neat list of resources in your deployment. You can then pick a specific one from the list to do more operations if needed.

**Key Takeaways:**

The `terraform state list` command is your go-to for checking out what resources are hanging out in your Terraform state. It's like looking at a manifest of your infrastructure – simple, but super helpful!
