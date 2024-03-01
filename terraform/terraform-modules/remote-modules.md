---
description: >-
  Learn what remote modules are and how you can work with them in your Terraform
  project.
---

# Remote Modules

In Terraform, remote modules are a powerful feature that allows you to share and reuse configuration blocks externally. Instead of keeping modules locally, you can store them on platforms like GitHub, BitBucket, or S3. Let's delve into an example to showcase the usage of a remote module.

#### Example:

```hcl
provider "aws" {
    region = "us-east-2"
}

module "work_queue" {
    source     = "github.com/kevholditch/sqs-with-backoff"
    queue_name = "work-queue"
}

output "work_queue" {
    value = module.work_queue.queue
}

output "work_queue_dead_letter_queue" {
    value = module.work_queue.dead_letter_queue
}
```

This code is similar to our previous local module example, with the key distinction being the use of a remote module. Here, we've set the `source` attribute to the GitHub repository URL (`github.com/kevholditch/sqs-with-backoff`), and Terraform automatically appends `https://` to the URL.

#### Output:

When you initialize Terraform using `terraform init`, it downloads the remote module. The output will indicate the module initialization and cloning process:

```plaintext
Initializing modules...
Downloading github.com/kevholditch/sqs-with-backoff for work_queue...
- work_queue in .terraform/modules/work_queue
```

#### Remote Module Cloning:

Terraform clones the remote module's code during initialization, and it's stored in the `.terraform/modules` directory. The code can be cloned via HTTPS or SSH, depending on your preference. If you choose SSH, ensure that your GitHub SSH setup is configured.

#### Running the Project:

Execute `terraform apply` to create the SQS queues, just as in the local module example. Two SQS queues will be created, with one acting as the dead letter queue for the other.

#### Remote Module Disadvantage:

When collaborating in a team and using remote modules from a platform like GitHub, there's a potential drawback. By default, Terraform fetches the latest version of the module every time it runs. This lack of version control can lead to unexpected changes if someone updates the module.

#### Solution to the Problem:

To address this, you can pin the version of the remote module by using a git tag. A git tag serves as a marker to a specific commit, ensuring that you control when to move to a newer version. By referencing a specific tag, you prevent unintended changes caused by updates to the master branch.

#### Update Example Code:

Update the `source` URL to include a reference to a specific tag, like `?ref=0.0.2`. This ensures Terraform uses the source code from the commit associated with the tagged version.

```hcl
module "work_queue" {
    source     = "github.com/kevholditch/sqs-with-backoff?ref=0.0.2"
    queue_name = "work-queue"
}
```

Running `terraform init` and `terraform apply` will now reflect the version specified by the tag, providing better control over module updates.

This approach allows you to consciously manage module versions, enhancing stability and predictability in collaborative environments.
