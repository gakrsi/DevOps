---
description: Learn about the plugin-based architecture of Terraform.
---

# Plugin-based Architecture

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption><p>Terraform architecture</p></figcaption></figure>

**Terraform's Core Structure:** Terraform, coded in Go (Golang), is packaged as a single binary with essential components for interpreting and deploying configurations. Instead of embedding codes for various providers and provisioners, Terraform relies on plugins. These plugins function as separate processes, communicating with the core Terraform binary through an RPC interface.

**Plugin Architecture:** To enhance flexibility and avoid bloating the binary, HashiCorp adopted a plugin architecture. This approach allows providers to update independently, preventing the need for a new Terraform version each time a feature is added or modified.

**Demonstration Using Multiple Providers:**

**Multiple Different Providers:**

```hcl
provider "aws" {
  region = "us-east-1"
}

resource "random_integer" "rand" {
  min = 10000
  max = 99999
}

resource "aws_s3_bucket" "bucket" {
  name = "unique-name-${random_integer.rand.result}"
  ...
}
```

* Configurations often involve different providers. For instance, an AWS provider and a random provider can be used together in a configuration.
* Explicitly define a provider in a block or imply it through resource usage.

**Multiple Instances of a Provider:**

```hcl
provider "aws" {
  region = "us-east-1"
}

provider "aws" {
  region = "us-west-2"
  alias = "west"
}

resource "aws_ec2_instance" "example-west" {
  name = "instance2"
  provider = aws.west
  ...
}
```

* Instances of the same provider may be needed, e.g., different AWS regions.
* Utilize the alias meta-argument to reference specific instances of a provider.
* This is crucial for scenarios like working with multiple subscriptions in Azure or varied master hosts in Kubernetes.

**Use Cases and Considerations:**

* Provider aliases are useful for specifying which instance of a provider to use.
* Aliases can be applied in resource blocks, and even with modules, ensuring clarity in complex configurations.

**Key takeaways:**

* Terraform leverages plugins for providers and provisioners rather than incorporating them into the core binary.
* This plugin-based approach keeps the Terraform binary compact, reduces the potential attack surface, and simplifies debugging.
* A configuration can involve multiple providers or instances of the same provider, understanding the alias argument is crucial.
* Provider aliases, especially when working with modules, play a vital role in specifying instances within the configuration.
