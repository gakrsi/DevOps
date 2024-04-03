---
description: Learn about Terraform's state locking behavior.
---

# Outline State Locking

### Why does Terraform lock the state? <a href="#why-does-terraform-lock-the-state" id="why-does-terraform-lock-the-state"></a>

State data is rather important, and transactions that involve the state should be atomic in nature. To prevent multiple processes from editing the state at the same time, Terraform locks the state.

### State locking behavior <a href="#state-locking-behavior" id="state-locking-behavior"></a>

Any operation that could edit the state first checks to make sure the state isn’t locked. If the state isn’t locked, Terraform attempts to create a lock on the state before making changes. Terraform doesn’t continue if it can’t attain a lock. We can override the locking behavior for several commands by using the `-lock=false` flag. This is a major change and should be approached with caution. A corrupted state is disastrous at best.

A `-lock-timeout` flag for most commands determines how long Terraform should wait to attain a lock on the state. This is useful for a state back-end that takes longer to create a lock for Terraform.

The majority of state back-ends support locking, but a few don’t. We should check the documentation for any given back-end to determine what features it supports.

### Key takeaways <a href="#key-takeaways" id="key-takeaways"></a>

Terraform can lock the state file on supported back-ends to prevent simultaneous write operations to the state data.
