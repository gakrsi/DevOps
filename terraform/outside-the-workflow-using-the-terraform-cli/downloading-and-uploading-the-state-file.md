---
description: Learn the pull and push subcommands and when they’re used in Terraform state.
---

# Downloading and Uploading the State File

**The "terraform state pull" Subcommand:**

The "terraform state pull" command allows you to manually retrieve and display the state from a remote or local backend. This command works for both remote and local backends.

**Syntax:** The syntax for the "pull" subcommand is as follows: `terraform state pull [options]`.

This command essentially lets you view the Terraform state directly, in a read-only mode. The output is provided in JSON format. You can use the following commands to save and view the state:

```bash
cp terraform.tfstate tfstate-file-download.json 
cat tfstate-file-download.json
```

The primary purpose of the "pull" subcommand is to inspect the contents of the remote state. If you're using a local backend, you could achieve the same by using `cat` on the local state file.

**Example Usage:** To read the content of the remote state, use the following command:

```bash
terraform state pull
```

**The "terraform state push" Subcommand:**

The "terraform state push" command is employed to manually upload a local state file to a remote backend. This command is applicable for both remote and local backends.

**Syntax:** The syntax for the "push" subcommand is as follows: `terraform state push [options] PATH`.

**Arguments:** The `PATH` argument specifies the local path of the file to be pushed to the remote state. You can also use `stdin` as the `PATH` by specifying the value `-`.

**Caution:** Using the "push" subcommand is considered risky. It involves replacing the remote state with the contents of a local file, which can be a dangerous process.

**Prevention Measures:** Terraform implements safety checks to prevent inadvertent actions. If the lineage value in the state is different or the serial value of the destination state is higher than the local state, Terraform blocks the push. The lineage and serial values indicate potential configuration differences or outdated data.

**Force Option:** If you are absolutely certain about your action, you can use the `-force` flag to override the safety checks, allowing Terraform to overwrite the remote state.

**Key Takeaways:**

* The "terraform state pull" subcommand is mainly used to examine the contents of the remote state.
* The "terraform state push" subcommand enables the manual upload of a local state file to a remote backend. Exercise caution and consider safety measures due to the potential risks involved.
