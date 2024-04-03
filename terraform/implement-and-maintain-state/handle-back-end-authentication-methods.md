---
description: Learn how Terraform handles the backend authentication methods.
---

# Handle Back-end Authentication Methods

### Back-end authentication <a href="#back-end-authentication" id="back-end-authentication"></a>

Some back-ends require authentication and authorization to access state data stored in the backend. For instance, Azure Storage requires access keys, and the MySQL back-end requires database credentials. The documentation for each back-end type will list out the exact format and type of authentication required.

Let’s look at the Azure Storage backend as an example:

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

Azure Storage accounts have an access key that allows full access to the contents of a storage account. In the code snippet above, the access key value is stored directly in the configuration. Generally speaking, this isn’t a recommended practice.

### Define credentials in a configuration <a href="#define-credentials-in-a-configuration" id="define-credentials-in-a-configuration"></a>

Statically defining credentials in a configuration presents a couple of issues. We may want to update the credentials on a regular basis, which involves updating the configuration each time. It’s also not a wise idea to store important credentials in clear text on the local workstation or in source control. That presents a potentially major security concern.

Someone might define AWS keys in a Terraform configuration and then accidentally check that configuration into a public GitHub repository, exposing their AWS keys to the entire world. This is a rather common occurrence.

### Define credentials using Terraform variables <a href="#define-credentials-using-terraform-variables" id="define-credentials-using-terraform-variables"></a>

We can’t define the credentials for a back-end using Terraform variables. The back-end is evaluated during initialization before variables are loaded or evaluated. Because the variables haven’t been evaluated, Terraform has no idea they exist, let alone what value is stored in them. For that reason, Terraform can’t use the values defined in variables for our back-end configuration.

The solution is to use a partial back-end configuration in the root module and provide the rest of the information at runtime. We’ll discuss partial configurations in more detail further on in the [the-backend-block-in-configuration.md](the-backend-block-in-configuration.md "mention") when we explore the `backend` configuration block.

### Key takeaways <a href="#key-takeaways" id="key-takeaways"></a>

Remote back-ends usually require authentication. We need to supply that information in the `backend` configuration or at runtime.
