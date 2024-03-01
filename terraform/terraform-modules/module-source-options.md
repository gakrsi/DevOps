---
description: Learn about the Terraform module and its source options.
---

# Module Source Options

#### What is a Terraform Module?

A Terraform module is like a set of instructions neatly packed together. It doesn't need to have everything—inputs, resources, and outputs are optional! Imagine a folder filled with `.tf` or `.tf.json` files—that's your module. The main set of instructions you're working with is the root module. If it needs extra help, it can call other modules to create resources.

#### Understanding Terraform Module Hierarchy

Modules are like a family tree, where the root module calls a child module, which might call another child module. Picture a root module calling a child module (let's say, `lb-vms`) to build a load-balanced cluster of Azure virtual machines. Now, this `lb-vms` module might bring in a `vnet` module to create the needed VNet and subnets for the cluster. If you peeked at `terraform state list`, you might see a resource address like `module.lb-vms.module.vnet.azurerm_subnet.subnet[0]`.

To make this happen, you use the `module` script block keyword, adding a name label like `module <name_label> {}`. The module calling the code block is the calling module, while the one being called is the child module.

#### Where Modules Come From

To use a module, Terraform needs to know where to find its files. The `source` argument in the module block shows where the module files live. These files can be stored in various places:

* Local paths
* Terraform Registry
* GitHub
* Bitbucket
* Generic Git, Mercurial repositories
* HTTP URLs
* S3 buckets
* GCS buckets

Especially noteworthy is the Terraform Registry at `registry.terraform.io`. It's a hub of verified modules maintained by third-party vendors. Think AWS VPCs or Azure AKS clusters. Because they're vetted by the vendors, you can trust these modules to work as expected.

When your source is a remote place, Terraform brings the files to the local `.terraform` directory during `terraform init.` You can also use `terraform get` to grab modules separately.

As for where you store your modules, HashiCorp suggests keeping closely tied ones with your configuration. If it's a module others might use, store it in a shared place, either public or private.

#### Key takeaways

* Modules are like LEGO sets of configurations.
* The source of a module can be local or remote, including the Terraform Registry.
* Verified modules on the Terraform Registry are like gold—you can trust them.
