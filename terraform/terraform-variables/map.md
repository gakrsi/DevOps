---
description: We will learn how to use Map type constraints in your Terraform project.
---

# Map

A map is a collection of values organized and accessible through key names. You can define the type of values the map will hold.

```hcl
variable "my_map" {
    type    = map(number)
    default = {
        "alpha" = 2
        "bravo" = 3
    }
}

output "map" {
    value = var.my_map
}

output "alpha_value" {
    value = var.my_map["alpha"]
}
```

we're constructing a map specifically designed to hold numbers. The map is initialized with two keys, "alpha" and "bravo," with corresponding values 2 and 3. The declaration of the map's type as (number) ensures that all values within the map conform to this numerical constraint.

Map Output Value: The output value of the map will display the entire map, showcasing the key-value pairs within.

To extract a specific value from the map, we utilize the \[] syntax. The "alpha\_value" output will present the value associated with the "alpha" key in the map, which, in this case, is 2. This illustrates the ability to selectively access and display individual values within a map based on their assigned keys.
