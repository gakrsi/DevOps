---
description: >-
  HashiCorp Configuration Language (HCL) is Terraform' s foundational syntax,
  comprising two essential constructs: Arguments and Blocks.
---

# Introduction to Terraform HCL

In the context of HCL:

**Arguments:** Assign values to specific names, exemplified by `image_id = "abc123"`. The identifier before the equals sign denotes the argument name, while the expression afterward represents the argument's value.

```hcl
image_id = "abc123"
```

**Blocks:** Containers for content, like the `resource "aws_instance" "example"` example. Blocks have types (e.g., resource) and may include labels, creating a nested hierarchy defined by { and }.

```hcl
resource "aws_instance" "example" {
  ami = "abc123"

  network_interface {
    # ...
  }
}
```

**Identifiers:** Names for arguments, block types, and Terraform constructs. They can include letters, digits, underscores (\_), and hyphens (-), with the first character being a letter.

**Comments:** Three syntaxes&#x20;

* \# for single-line comments
* // as an alternative
* /\* and \*/ for multi-line comments.

> Notably, the # style is recommended, as automatic formatting tools often convert // to # due to its idiomatic usage.
