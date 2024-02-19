---
description: >-
  This lesson will teach you how to set defaults in Terraform variables and
  their use.
---

# Variable Defaults

Consider a project where we want to create an AWS S3 bucket. In this example:

```hcl
provider "aws" {
  region = "us-east-2"
}

variable "bucket_name" {
  description = "The name of the bucket you want to create"
}

variable "bucket_suffix" {
  default = "-abcd"
}

resource "aws_s3_bucket" "bucket" {
  bucket = "${var.bucket_name}${var.bucket_suffix}"
}
```

Now, we've extended the project by adding a new variable, "bucket\_suffix," with a default value of "-abcd." If you don't provide a specific value for this variable, Terraform will use the default value. The bucket name is then constructed by combining the values of "bucket\_name" and "bucket\_suffix."

To clarify, when using variables inside a string, we use `${}` to tell Terraform to substitute the actual values. Otherwise, Terraform would treat it as plain text and print the variable names instead of their values.

In summary, this Terraform project creates an S3 bucket in the "us-east-2" region. You can customize the bucket name using the "bucket\_name" variable and have an optional suffix provided by the "bucket\_suffix" variable with a default value of "-abcd." This makes your infrastructure code more flexible and adaptable to different scenarios.
