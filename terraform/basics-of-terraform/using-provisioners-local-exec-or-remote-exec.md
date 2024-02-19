---
description: >-
  Learn the basics of Terraform provisioners and when to use local and remote
  provisioners.
---

# Using Provisioners, local-exec, or remote-exec

When creating a resource, you might want to execute certain scripts or operations either locally or on the remote resource. Terraform provisioners serve this purpose, though they somewhat deviate from Terraform's declarative and idempotent model. Provisioner execution lacks atomicity and idempotence, as it involves running arbitrary scripts or instructions. Terraform cannot effectively track the results and status of provisioners as it does for other resources. Hence, HashiCorp advises resorting to provisioners only as a last option.

**Use Cases:** Provisioners serve three primary use cases:

1. **Loading data into a virtual machine.**
2. **Bootstrapping a virtual machine for a config manager.**
3. **Saving data locally on the system.**

The remote-exec provisioner facilitates connecting to a remote machine via WinRM or SSH to run a script remotely. Note that the target machine must accept remote connections. Instead of relying on remote-exec to pass data to a virtual machine, cloud providers' tools like `user_data` in AWS or `custom_data` in Azure are recommended. All major public clouds support data exchange methods that don't require direct remote access to the machine.

Besides remote-exec, provisioners for Chef, Puppet, Salt, and other configuration managers are available. They enable bootstrapping the virtual machine to use the preferred config manager. A more efficient approach is to create a custom image with the config manager software pre-installed and register it with the config management server during bootup, utilizing the mentioned data loading options.

To run a script locally within the Terraform configuration, the `local-exec` provisioner can be employed. However, if a provider already offers the desired functionality, like the Local provider interacting with local files, it is advisable to use that instead. Yet, there might be scenarios where a local script remains the only viable option.

**Example Usage:**

Below are examples showcasing different provisioners:&#x20;

{% code lineNumbers="true" %}
```hcl
resource "aws_instance" "web" {
  # ...
  provisioner "local-exec" {
    command = "echo The server's IP address is ${self.private_ip}"
  }
}

```
{% endcode %}

{% code lineNumbers="true" %}
```hcl
resource "aws_instance" "web" {
  # ...
  provisioner "local-exec" {
    command = "echo ${self.private_ip} >> private_ips.txt"
  }
}

```
{% endcode %}

{% code lineNumbers="true" %}
```hcl
resource "aws_instance" "web" {
  # ...
  provisioner "remote-exec" {
    inline = [
      "puppet apply",
      "consul join ${aws_instance.web.private_ip}",
    ]
  }
}

```
{% endcode %}

To avoid these challenges, it is recommended to use provisioners only as a last resort. The `remote-exec` provisioner runs scripts on the remote machine through WinRM or SSH, while `local-exec` runs scripts on the local machine.
