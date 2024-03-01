---
description: Learn about module input variables.
---

# Module Inputs

#### Understanding Terraform Module Inputs

Input variables in Terraform modules act like settings or parameters, allowing you to customize the behavior of a module without tweaking its internal code. This customization capability is crucial when you want to reuse modules across different configurations.

**Passing Inputs to a Module**

When using a module, you can supply input values in the module block of your configuration. These inputs can come from variables defined in the root module, hardcoded values in the configuration, or even values fetched from other resources.

```hcl
module "vpc" {
  source = "terraform-aws-modules/vpc/aws"

  name            = "${var.prefix}-vpc"
  cidr            = var.cidr_address
  azs             = var.vpc_azs
  private_subnets = var.vpc_private_subnets
  public_subnets  = var.vpc_private_subnets
}
```

Here, we're providing inputs to the official `vpc` module from the Terraform Registry.

**Declaring Input Variables in a Module**

Just like how you define variables in the root module, input variables in a child module need to be declared using a variable block. Let's peek into the `variables.tf` file of the official `vpc` module:

```hcl
variable "name" {
  description = "Name to be used on all the resources as identifier"
  type        = string
  default     = ""
}

variable "cidr" {
  description = "The CIDR block for the VPC. Default value is a valid CIDR, but not acceptable by AWS and should be overridden"
  type        = string
  default     = "0.0.0.0/0"
}
```

Here, we're defining two input variables: `name` and `cidr`.

**Input Variable Details**

* **Variable Name:** This is the label after the `variable` keyword. It's a unique identifier for the variable, used to assign and reference its value.
* **Type Argument:** Optionally, you can specify a type for the variable, indicating what kind of value it should accept. It could be a string, a list of integers, or even an entire resource.
* **Default Argument:** If present, this makes the variable optional. The default value is used if no value is provided when calling the module.
* **Description Argument:** A helpful field to provide guidance when creating modules for others to use.

**Meta-arguments**

Terraform 0.13 introduced some advanced features like `for_each`, `count`, and `depends_on` for modules. These meta-arguments enable more sophisticated control over how modules are instantiated and their dependencies.

#### Key takeaways

* **Flexible Customization:** Input variables allow you to tailor a module's behavior without altering its internal code.
* **Declaration Similarity:** Declaring input variables in modules mirrors the process in the root module.
* **Advanced Module Control:** Meta-arguments bring advanced features for module instantiation and dependency management.
