---
description: Learn about the configuration of the Terraform backend block.
---

# The backend Block in Configuration

### How is the Terraform `backend` block defined? <a href="#how-is-the-terraform-backend-block-defined" id="how-is-the-terraform-backend-block-defined"></a>

The configuration of Terraform back-ends is defined inside the `terraform` block of a root module. The nested `backend` block defines the type of back-end being used and the required and optional properties of that back-end. Only one back-end can be specified per configuration. We can’t simultaneously store our state in two different back-ends or split our state across two different back-ends. That situation can be solved by splitting the configuration itself into two interdependent configurations.

As we saw earlier, a basic `backend` configuration block using Azure Storage might look like this:

```hcl
terraform
terraform {
  backend "azurerm" {
    storage_account_name = "arthurdent42"
    container_name       = "tfstate"
    key                  = "terraform.tfstate"
    access_key           = "qwertyuiop12345678..."
  }
}
```

### Best practices for partial configurations <a href="#best-practices-for-partial-configurations" id="best-practices-for-partial-configurations"></a>

Storing the storage account name and the access key directly in the configuration is probably not a good idea. But Terraform doesn’t allow the use of variables or any other interpolation in a `backend` configuration block. The alternative is to omit the settings we’d like to dynamically configure and instead supply them at runtime. The resulting block is called a **partial configuration.**

Our example above would look like this:

```hcl
terraform
terraform {
  backend "azurerm" {
    container_name = "tfstate"
    key            = "terraform.tfstate"
  }
}
```

The values for `storage_account_name` and `access_key` can be supplied in one of four ways:

1. They can be supplied interactively at the command line when we run `terraform init`.
2. They can be supplied through the `-backend-config` flag with a set of key/value pairs.
3. They can be supplied through the `-backend-config` flag with a path to a file with key/value pairs.
4. They can be supplied using environment variables defined by the `backend` type.

Some arguments in a back-end can be sourced from environment variables. For instance, using Managed Services Identity (MSI) for Azure Storage can be configured by setting `ARM_USE_MSI` to `true`. We need to check the back-end documentation to see which settings are supported by environment variables.

After the first time we run `terraform init` with our back-end values, we don’t have to supply the values again for other commands. The back-end information and other initialization data are stored in a local file in the `.terraform` subdirectory of our configuration. This directory should be exempted from source control because our back-end configuration may have sensitive data in it, like authentication credentials.

When we create a new repository on GitHub and create a `.gitignore` file, we can select Terraform as one of the options. It automatically excludes the `.terraform` directory, as well as files like `terraform.tfvars` and `terraform.tfstate`. We should use `.gitignore` on any new project with those exemptions.

### Key takeaways <a href="#key-takeaways" id="key-takeaways"></a>

Terraform backends are defined using a `backend` configuration block. Partial configurations should be used to omit sensitive and dynamic values, which are submitted at runtime.
