---
description: >-
  Learn about the types of Terraform providers and how they can be added to the
  code block.
---

# How Terraform Finds and Fetches Providers

**Evolution in Provider Management:** Understanding how Terraform discovers and fetches providers, especially after version 0.13, is crucial. This lesson delves into the earlier methods and how they've evolved in the latest version.

**Provider Categories:** Before version 0.13, providers were classified as HashiCorp distributed or independent third-party. HashiCorp providers were automatically downloaded during initialization, while third-party ones could be placed in a local plugins directory.

**Types of Providers in v0.13:** Version 0.13 brings a change, allowing automatic downloads from public or private repositories. Three types emerge in the official public repository - Official (by HashiCorp), Verified (partner-maintained), and Community (individuals).

**Adding Providers in Terraform Code:** Providers are incorporated through a `required_providers` nested block within the terraform code. Local names, sources, and versions are specified. For instance:

```hcl
terraform {
  required_providers {
    aws = {
      source = "hashicorp/aws"
      version = "~> 3.0"
    }
  }
}
```

**Using Locally Developed Providers:** Organizations opting for locally developed providers can use the `source` argument, pointing to a local path. Terraform checks these locations during initialization.

**Improving Performance with Plugin Caching:** To enhance performance, plugin caching is employed through `plugin_cache_dir` or `TF_PLUGIN_CACHE_DIR` to reduce download times by checking the cache before fetching from the internet.

**Pointing Plugins to Internal Locations:** For scenarios where internet access is restricted, plugins can be directed to internal locations through mirrors or local directories. This is achieved by configuring mirror paths or manually downloading and specifying plugin directories.

**Key takeaways:**

* Terraform automatically downloads plugins from identified sources during configuration initialization.
* Private plugins can reside in repositories or mirror folders.
* Performance enhancements include plugin caching and specifying directories containing plugins.
