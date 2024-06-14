---
description: Learn how to add a Helm repository.
---

# Adding Helm Repository

Before installing a Helm chart, it's essential to connect to the repository where the chart is hosted. Here’s how you can manage Helm repositories using the CLI:

**Listing Helm Repositories**

To view the current repositories configured in Helm:

```bash
helm repo list
```

This command will display a list of repositories along with their URLs.

**Adding a Helm Repository**

To add a new repository to Helm:

```bash
helm repo add [NAME] [URL]
```

For example, to add the Kubernetes Dashboard repository:

```bash
helm repo add kubernetes-dashboard https://kubernetes.github.io/dashboard/
```

This command associates the name `kubernetes-dashboard` with the URL where the Helm charts are hosted.

**Updating Repositories**

After adding a new repository, refresh Helm's local list of repositories:

```bash
helm repo update
```

This ensures that Helm has the latest information about available charts in all configured repositories.

**Additional Repository Management Options**

For advanced configuration and management of Helm repositories, you can use flags with the `helm repo add` command:

```bash
helm repo add --help
```

```
add a chart repository

Usage:
  helm repo add [NAME] [URL] [flags]

Flags:
      --allow-deprecated-repos     by default, this command will not allow adding official repos that have been permanently deleted. This disables that behavior
      --ca-file string             verify certificates of HTTPS-enabled servers using this CA bundle
      --cert-file string           identify HTTPS client using this SSL certificate file
      --force-update               replace (overwrite) the repo if it already exists
  -h, --help                       help for add
      --insecure-skip-tls-verify   skip tls certificate checks for the repository
      --key-file string            identify HTTPS client using this SSL key file
      --no-update                  Ignored. Formerly, it would disabled forced updates. It is deprecated by force-update.
      --pass-credentials           pass credentials to all domains
      --password string            chart repository password
      --password-stdin             read chart repository password from stdin
      --username string            chart repository usernamee
```

This command provides detailed information about available flags, such as `--ca-file`, `--username`, `--password`, and others, which can be used to configure authentication, TLS verification, and repository behavior.

By following these steps, you can seamlessly manage Helm repositories and install Helm charts from various sources, enabling effective Kubernetes application deployment and management.
