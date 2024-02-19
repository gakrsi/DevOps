---
description: >-
  Learn how to format the Terraform configuration files using the terraform fmt
  command.
---

# Formatting the Code

* **Purpose of `terraform fmt`**:
  * Rewrites Terraform configuration files to a canonical format and style.
  * Applies a subset of Terraform language style conventions and makes minor adjustments for readability.
* **Consistency and Style Enforcement**:
  * Commands generating Terraform configurations adhere to the style imposed by `terraform fmt`.
  * Ensures consistency across different Terraform codebases.
* **Handling Terraform Version Changes**:
  * Canonical format may undergo minor changes between Terraform versions.
  * Recommended to run `terraform fmt` after upgrading Terraform to maintain consistency.
* **Non-Breaking Changes**:
  * New formatting rules in `terraform fmt` are not considered breaking changes.
  * Aim to apply more rules already present in documented examples.
* **Opinionated and Unmodifiable**:
  * `terraform fmt` is intentionally opinionated with no customization options.
  * Primary goal is to encourage consistent style across codebases.
* **Recommended Usage**:
  * Follow `terraform fmt` style conventions when writing Terraform modules.
  * Disagreements with results are subjective, and if objectionable, users can choose not to use the command.
* **Third-Party Tools and Consistency**:
  * If not using `terraform fmt`, consider third-party formatting tools.
  * Apply the chosen tool to both manually written and automatically generated files for consistency.
* **Usage Syntax**:
  * `terraform fmt [options] [target...]`
  * Default behavior: Scans current directory for configuration files.
  * Optional target argument: Specifies directory or file for scanning.
  * Use a single dash (`-`) to read from standard input (STDIN).
* **Command-Line Flags**:
  * `-list=false`: Do not list files with formatting inconsistencies.
  * `-write=false`: Do not overwrite input files (implied by `-check` or when input is STDIN).
  * `-diff`: Display diffs of formatting changes.
  * `-check`: Check if input is formatted, exit status indicates proper formatting.
  * `-recursive`: Process files in subdirectories in addition to the given directory or current directory.
