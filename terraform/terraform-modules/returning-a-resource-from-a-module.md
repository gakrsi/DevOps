---
description: This lesson will teach how to return a whole resource from a module.
---

# Returning a resource from a module

You can retrieve a complete resource from a module, enabling users to access all its fields. In our example, we'll enhance the SQS backoff module to return the entire SQS queue and its dead-letter queue.

#### Project Structure:

```css
sqs-with-backoff/
   variables.tf
   outputs.tf
   main.tf
main.tf
```

#### Updating `outputs.tf`:

We modify the `outputs.tf` file inside the `sqs-with-backoff` directory as follows:

```hcl
output "queue" {
    value = aws_sqs_queue.sqs
}

output "dead_letter_queue" {
    value = aws_sqs_queue.sqs_dead_letter
}
```

#### Explanation:

We set the value of the `queue` output to the entire `aws_sqs_queue.sqs` SQS queue resource, including all its attributes. Similarly, the `dead_letter_queue` output returns the complete `aws_sqs_queue.sqs_dead_letter` resource.

#### Updating Top-Level `main.tf`:

In the main `main.tf` file, we replace all output blocks with:

```hcl
output "work_queue" {
    value = module.work_queue.queue
}

output "work_queue_dead_letter_queue" {
    value = module.work_queue.dead_letter_queue
}
```

#### Explanation:

These output blocks in the top-level `main.tf` file now return the complete SQS queue and dead-letter queue resources from the `work_queue` module.

#### Simplifying Output Blocks:

```plaintext
1. Output "work_queue": 
Returns the entire SQS queue resource created by the module.
2. Output "work_queue_dead_letter_queue":
Returns the entire dead-letter queue resource created by the module.
```

This approach provides users with access to all attributes of the created resources, enhancing flexibility and usability.
