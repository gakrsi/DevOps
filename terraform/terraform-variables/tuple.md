---
description: We will learn how to use Tuple type constraints in your Terraform project.
---

# Tuple

A tuple is a collection of values with a rigid structure, where each value is strongly typed. In simpler terms, it's like a predefined list with a specific number of values, each adhering to a defined type and order.

```hcl
variable "my_tup" {
    type    = tuple([number, string, bool])
    default = [4, "hello", false]
}

output "tup" {
    value = var.my_tup
}
```

In this Terraform code, we create a tuple variable named "my\_tup" with three distinct values:

1. A number
2. A string
3. A boolean

The syntax for defining a tuple uses the form `tuple([TYPE, TYPE...])`. As emphasized earlier, when specifying a tuple with three values, it must be assigned a value consisting of three elements. Hence, the initialization as \[4, "hello", false].

Upon execution, the output resembles that of a list. Conceptually, think of a tuple as a predefined list with a fixed length, ensuring each element maintains a specific type.

Experimenting with the tuple, try adding an extra value to its default (e.g., \[4, "hello", false, "hey"]). Attempting a Terraform apply will result in an error. Terraform enforces adherence to the tuple's definition, ensuring the specified length and types match precisely. This showcases the strictness and structure that tuples bring to data representation.

\
