---
description: This lesson will address Terraform variables and their uses.
---

# Terraform Variables

In Terraform, variables serve as placeholders for dynamic values that can be used throughout your infrastructure code. They allow you to abstract and generalize your configurations, making them more adaptable to different environments and scenarios. Variables can be used to define various types of values, including strings, numbers, lists, and maps.

### **Declaring a Variable:**

* When you want to use some information that might change, like a name or a list of items, you declare it as a variable.
* In Terraform, you declare a variable using the `variable` keyword and put a name for it inside quotes. Let's say we're using the name "bucket\_name" as our variable.

```hcl
variable "bucket_name" { description = "A name for our S3 bucket" }
```

* You can also declare a variable without specifying a description:

```hcl
variable "bucket_name" {}
```

* Adding a description is optional, but it helps users understand what the variable is for.

### **Using the Variable:**

* Once you've declared a variable, you can use its value in your Terraform code using `var.<variable_name>`.
* For example, if you have an S3 bucket resource and you want to set its name based on your variable, you would do something like this:

```hcl
resource "aws_s3_bucket" "my_bucket" {
  bucket = var.bucket_name
  # other bucket properties...
}
```

* This tells Terraform to use the value you provide for `var.bucket_name` as the name for your S3 bucket.
* Note: Providing a description for your variables is a good practice. It helps users understand what kind of values are expected and how the variable will be used in your Terraform configuration.

In summary, declaring a variable is like saying, "Hey, I might want to change this later," and using a variable is like telling Terraform, "Use whatever value I give for this variable in the specific part of the configuration where I need it." Adding descriptions helps make your code more understandable for both you and others who might work on the project.
