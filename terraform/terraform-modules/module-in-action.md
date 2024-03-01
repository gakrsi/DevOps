---
description: Learn how to work with modules in detail.
---

# Module in action

#### Folder Structure:

```plaintext
plaintextCopy codesqs-with-backoff/
    main.tf
    variables.tf
    output.tf
main.tf
variable.tf
```

#### Module Explanation:

1.  **Variables (`variables.tf`):**

    ```hcl
    variable "queue_name" {
        description = "Name of queue"
    }

    variable "max_receive_count" {
        description = "The maximum number of times that a message can be received by consumers"
        default     = 5
    }

    variable "visibility_timeout" {
        default = 30
    }
    ```
2.  **Module Definition (`main.tf` in `sqs-with-backoff/`):**

    ```hcl
    resource "aws_sqs_queue" "sqs" {
        name                        = "awesome_co-${var.queue_name}"
        visibility_timeout_seconds  = var.visibility_timeout
        delay_seconds               = 0
        max_message_size            = 262144
        message_retention_seconds   = 345600 # 4 days.
        receive_wait_time_seconds   = 20 # Enable long polling
        redrive_policy              = "{\"deadLetterTargetArn\":\"${aws_sqs_queue.sqs_dead_letter.arn}\",\"maxReceiveCount\":${var.max_receive_count}}"
    }

    resource "aws_sqs_queue" "sqs_dead_letter" {
        name                       = "awesome_co-${var.queue_name}-dead-letter"
        delay_seconds              = 0
        max_message_size           = 262144
        message_retention_seconds  = 1209600 # 14 days.
        receive_wait_time_seconds  = 20
    }
    ```
3.  **Outputs (`output.tf`):**

    ```hcl
    output "queue_arn" {
        value = aws_sqs_queue.sqs.arn
    }

    output "queue_name" {
        value = aws_sqs_queue.sqs.name
    }

    output "dead_letter_queue_arn" {
        value = aws_sqs_queue.sqs_dead_letter.arn
    }

    output "dead_letter_queue_name" {
        value = aws_sqs_queue.sqs_dead_letter.name
    }
    ```

#### Usage in Top-Level Terraform Configuration (`main.tf`):

```hcl
provider "aws" {
    region = "eu-west-1"
}

module "work_queue" {
    source     = "./sqs-with-backoff"
    queue_name = "work-queue"
}

output "work_queue_name" {
    value = module.work_queue.queue_name
}

output "work_queue_dead_letter_name" {
    value = module.work_queue.dead_letter_queue_name
}
```

#### Running the Project:

* Run `terraform init` and `terraform apply` to create the SQS queues.
* The `work_queue_name` and `work_queue_dead_letter_name` outputs display the queue names.

#### Extending with Another Module Instance:

```hcl
module "thread_queue" {
    source     = "./sqs-with-backoff"
    queue_name = "thread-queue"
}
```

This adds another instance of the module, creating additional queues with different names.

#### Benefits of Modules:

1. **Code Reusability:**
   * Easily reuse the SQS module with different configurations across the project.
2. **Consistent Structure:**
   * Modules enforce a consistent structure, promoting naming conventions and organization.
3. **Easy Updates:**
   * Updating the module reflects changes across all instances, ensuring consistency.
4. **Reduced Redundancy:**
   * Avoid redundancy by defining common logic in a single module.

By structuring your Terraform code with modules, you enhance maintainability and scalability, allowing for efficient management of infrastructure components.
