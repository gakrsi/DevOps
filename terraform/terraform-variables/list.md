---
description: Learn how to use the Terraform type constraints List.
---

# List

A list is a versatile data structure that can contain elements of a specific type. For instance, you can create a list of strings like \["foo", "bar"] or a list of numbers \[2, 4, 7]. The specified type ensures that every element within the list adheres to that particular data type.

Project Example: Let's delve into an illustrative example:

```hcl
variable "a" {
    type    = list(string)
    default = ["foo", "bar", "baz"]
}

output "a" {
    value = var.a
}

output "b" {
    value = element(var.a, 1)
}

output "c" {
    value = length(var.a)
}
```

In this code snippet, we declare a variable "a" as a list of strings using the 'type' attribute. The default value for this list is set as \["foo", "bar", "baz"].

Output Variable Display:

* Output "a" straightforwardly prints the contents of the list.
* Variable "b" utilizes the built-in 'element' function, designed for list manipulation. In this case, it fetches the element at index 1, resulting in the output "bar."
* HCL language incorporates various built-in functions, and 'element' is one such tool for list operations.
* For Output "c," the 'length' function is employed. This function calculates the length of the list, so "c" outputs the value 3, signifying the number of elements in the list.

This coding example showcases the flexibility and functionality of lists in HashiCorp Configuration Language (HCL), where built-in functions like 'element' and 'length' facilitate efficient manipulation and retrieval of data from lists.
