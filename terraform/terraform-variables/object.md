---
description: We will learn how to use Object type constraints in your Terraform project.
---

# Object

An object in Terraform allows you to create structured entities by combining various types. These objects enable the definition of intricate structures while adhering to specified types. Let's delve into an example to better understand this concept.

```hcl
variable "person" {
    type    = object({ name = string, age = number })
    default = {
        name = "Bob"
        age  = 10
    }
}

output "person" {
    value = var.person
}

variable "person_with_address" {
    type    = object({ name = string, age = number,
        address = object({ line1 = string, line2 = string, 
                    county = string, postcode = string }) })
    default = {
        name    = "Jim"
        age     = 21
        address = {
            line1    = "1 the road"
            line2    = "St Ives"
            county   = "Cambridgeshire"
            postcode = "CB1 2GB"
        }
    }
}

output "person_with_address" {
    value = var.person_with_address
}
```

Object Definition: In the initial part of the project, we define a variable named "person." This variable consists of two fields: a "name" of type string and an "age" of type number. The object is defined by specifying each field within {} brackets, using the form fieldname = type. Default values, such as "Bob" and 10, are assigned to illustrate the concept. Executing the project will display the values assigned to the "person" output.

Type Constraints: Values are constrained by the types defined; attempting to assign a string to the "age" field would result in a type constraint error. Notably, Terraform allows items with the same identifier when they serve different purposes, as seen with the variable and output both named "person."

Building Complexity: To demonstrate nesting objects for increased complexity, a variable named "person\_with\_address" is introduced. It extends the previous "person" structure by adding an "address" field, which, in itself, is another object containing four strings: line1, line2, county, and postcode. Initialization involves wrapping these values in {} brackets. Executing the project will showcase the complete structure of "person\_with\_address."

This technique allows the step-by-step construction of intricate and layered structures, facilitating the creation of complex data models in Terraform.
