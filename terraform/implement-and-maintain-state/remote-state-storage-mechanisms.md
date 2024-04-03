---
description: Learn how Terraform stores state data in a remote location.
---

# Remote State Storage Mechanisms

Terraform uses a local file back-end by default. While that might be sufficient when working on a small independent project, it doesn’t provide data protection or allow for collaboration. The solution is to use a remote state back-end, which stores the state data in a remote shared location.

### Classes of back-ends <a href="#classes-of-back-ends" id="classes-of-back-ends"></a>

Remote back-ends store state data in a remote location based on the back-end configuration defined in the configuration. Not all back-ends are the same, and HashiCorp defines two classes of back-ends.

* **Standard** includes state management and possibly locking.
* **Enhanced** includes remote operations as well as standard features.

The enhanced remote back-ends are either Terraform Cloud or Terraform Enterprise. Both services allow us to run our Terraform operations—like `terraform plan` and `terraform apply`—on the remote service instead of locally.

### Supported standard backends <a href="#supported-standard-backends" id="supported-standard-backends"></a>

There are 14 standard back-ends as of now; detailing each is beyond the scope of this course. It’s recommended to check the documentation for each one to learn details about what features are supported and what values are required.

### Using a remote back-end <a href="#using-a-remote-back-end" id="using-a-remote-back-end"></a>

When state data is stored in a remote back-end, it isn’t written to disk on the local system. The state data is loaded into memory during Terraform operations and then flushed when no longer in use. Sensitive data within the state file is never stored on the local disk, providing an additional level of security if the local system is lost or compromised.

In addition to storing the state in a secure location, using a remote state also enables other team members to access or alter the state or use it as a data source. Let’s say that we’re collaborating with Joan the network admin on a network configuration. Both of us can update our local copy of the configuration and then push it to version control. When it’s time to update the actual environment, we run the plan and apply phases. The remote state is locked during the update, so Joan can’t make any changes. When Joan runs her next plan, it’ll be using the updated remote state data from our most recent apply.

### Accessing outputs <a href="#accessing-outputs" id="accessing-outputs"></a>

Any outputs defined in a configuration can be accessed using the state file as a data source. For instance, let’s say that an application team needs to query information about a network configuration. We could give them read-only access to the network state and ensure the information they need is exposed through outputs. The application team would then define the network state as a data source in their configuration and reference the outputs directly.

### Key takeaways <a href="#key-takeaways" id="key-takeaways"></a>

Terraform can store state data in a remote location that supports collaboration and state as a data source.
