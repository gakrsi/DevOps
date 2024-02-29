---
description: Learn how to use the Terraform type constraints Set.
---

# Set

A set is akin to a list, with a key distinction - a set exclusively accommodates unique values.

```hcl
variable "my_set" {
    type    = set(number)
    default = [7, 2, 2]
}

variable "my_list" {
    type    = list(string)
    default = ["foo", "bar", "foo"]
}

output "set" {
    value = var.my_set
}

output "list" {
    value = var.my_list
}

output "list_as_set" {
    value = toset(var.my_list)
}
```

In this example, we introduce a variable, "my\_set," initialized as the set \[7, 2, 2]. Notably, a set exclusively retains unique values. Consequently, when executing this project, the output value for the set will be \[7, 2], with Terraform automatically eliminating one of the duplicate "2" values.

To underscore the utility of sets, we create a list named "my\_list," deliberately repeating the value "foo" twice. The list output will be \["foo", "bar", "foo"], as my\_list, being of list type, allows duplicate values.

For the "list\_as\_set" output, the 'toset' function is employed to convert the variable "my\_list" to a set. The resultant output will be \["foo", "bar"], as Terraform, during the conversion, discards the duplicate value "foo," showcasing the effectiveness of sets in eliminating redundancies.
