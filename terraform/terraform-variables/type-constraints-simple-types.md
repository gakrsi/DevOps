---
description: This lesson will cover the types of variables used in Terraform.
---

# Type Constraints - Simple Types

### Type Constraints for Variables

Up until now, we've been setting variables without specifying their type, allowing them to assume any type. However, you can be more specific about variable types using type constraints. There are three simple types you can use:

1. **string**
2. **number**
3. **bool**

```hcl
variable "a" {
    type = string
    default = "foo"
}

variable "b" {
    type = bool
    default = true
}

variable "c" {
    type = number
    default = 123
}

output "a" {
    value = var.a
}

output "b" {
    value = var.b
}

output "c" {
    value = var.c
}
```

In this project, we've defined three variables (`a`, `b`, and `c`) with specific type constraints:

* `a` is a string.
* `b` is a boolean.
* `c` is a number.

We've set default values for these variables, making it convenient to start without explicitly providing values during Terraform execution.

**Using Type Constraints:**

By using type constraints, you ensure that a variable can only be set to values of the specified type. If you try to set a value that doesn't match the type constraint (e.g., setting `b` to "hello" or 123), Terraform will display an error.

**Quirks and Interpretation:**

There are some interesting quirks to note:

* When defining a boolean (`bool`), values like `true`, `false`, `"true"`, `"false"`, `"1"` (evaluates to true), and `"0"` (evaluates to false) are all valid.
* For numbers (`number`), any valid number is allowed, with or without quotes.
* When defining a string (`string`), any value in quotes is allowed.

Understanding these nuances helps ensure that your variables are assigned values that align with their intended types. It's a way to enhance clarity and prevent unintentional type mismatches in your Terraform configurations.
