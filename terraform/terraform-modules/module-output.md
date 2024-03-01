---
description: Learn about module output values.
---

# Module output

#### Making Sense of Terraform Outputs

Output values in Terraform play a crucial role in making information from resources available for external use. Let's simplify this concept.

#### Practical Uses of Output Values

1. **Sharing Information Within Modules:**
   * A child module can use outputs to share specific resource attributes with the calling module.
2. **CLI Output Enhancement:**
   * Outputs in the root module can display specific values in the CLI output after executing `terraform apply`.
3. **Remote State Accessibility:**
   * When utilizing remote state, other configurations can access root module outputs through a `terraform_remote_state` data source.

#### Why Outputs Matter

In a module, if you create a resource, the attributes of that resource are accessible within the module. However, these attributes aren't readily available for use by other modules or as a data source in remote state scenarios. Output values act as a bridge, allowing you to name, transform, and expose these attributes for external use. If something isn't defined as an output, it remains secluded within the module.

#### Defining an Output Value

To export a value from a module, you use an `output` block. Here's an example from the official VPC module:

```hcl
output "vpc_id" {
  description = "The ID of the VPC"
  value       = concat(aws_vpc.this.*.id, [""])[0]
}
```

**Output Components**

* **Output Name:**
  * This is the label following the `output` keyword. It must be a valid identifier. When in a root module, both the name and value are shown in the configuration run. In a child module, the calling module uses this name to reference the exposed value like `module.module_name_label.output_name_label`.
* **Output Arguments:**
  * The `description` argument provides information about what the output contains, aiding module users. It's especially useful when creating modules for wider use.
  * The `value` argument takes an expression, and its result is what gets returned to the user. Terraform 0.12 onward supports returning complex values, even entire resources.

#### Key takeaways

* **Access Control:** If you want attributes to be available to calling modules, expose them as outputs.
* **Versatility of Outputs:** Outputs can be both simple values and entire resource structures.
* **Informative Descriptions:** Using the `description` field is encouraged to guide users leveraging the module.

\
