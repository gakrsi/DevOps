---
description: Learn where and how Terraform stores its state data.
---

# Describe the Default Local Back-end

### What is a backend? <a href="#what-is-a-backend" id="what-is-a-backend"></a>

Terraform needs a location to store its state data, which is called a back-end. In the absence of an alternate configuration, it stores the state on the local filesystem where the configuration is stored. Let’s examine the typical folder structure for an example configuration:

```console
.
├── .terraform
├── main.tf
└── terraform.tfstate
```

This Terraform configuration has been initialized and run through `terraform plan` and `terraform apply`. As a result, the `.terraform` directory holds the plugins used by the configuration, and the `terraform.tfstate` file holds the state data about the configuration.

The location of the local state file can be altered using the command line flag `-state=statefile` for commands like `terraform plan` and `terraform apply`.

### Key feature of a workspace <a href="#key-feature-of-a-workspace" id="key-feature-of-a-workspace"></a>

Terraform workspace

The directory structure will be slightly different if we’re using Terraform workspaces. A key feature of workspaces is that every workspace maintains a separate state, allowing multiple environments to use the same Terraform configuration. Let’s say we created a workspace called `development` in our configuration.

```console
├── .terraform
├── main.tf
├── terraform.tfstate
└── terraform.tfstate.d
    └── development
        └── terraform.tfstate
```

Terraform creates a directory, `terraform.state.d`, and a subdirectory for each workspace. In each workspace directory is the `terraform.tfstate` file for that workspace. The default workspace continues to use the `terraform.tfstate` file in the root directory.\


```bash
# copy-paste following command to create workspace
terraform workspace new name # replace name with any workspace name
# to view the directory
tree
```

### Key takeaways <a href="#key-takeaways" id="key-takeaways"></a>

Terraform will use the root module directory to store state data if no alternative is specified.
