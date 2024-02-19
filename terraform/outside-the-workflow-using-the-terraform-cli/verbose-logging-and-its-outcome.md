---
description: Learn when to enable verbose logging and its outcomes.
---

# Verbose Logging and its Outcome

**Configuring Terraform Logging:**

Terraform provides the capability to generate detailed logs by adjusting the environment variable `TF_LOG` to a specific verbosity level.

**Log Levels:** There are five levels of logs, ranging from most verbose to least: TRACE, DEBUG, INFO, WARN, and ERROR. The logs are directed to stderr. If `TF_LOG` is set to an unrecognized level (e.g., `TF_LOG=HAMSTER`), Terraform defaults to the highest verbosity level, TRACE.

To redirect logs to a file, set the `TF_LOG_PATH` environment variable to the full path of the desired file location (e.g., `/var/logs/terraform/my_log.log`).

**Handling Terraform Crashes:** If Terraform encounters an executable crash, logs are sent to stderr as usual, and an additional log file is generated. This `crash.log` file contains debug logs, panic messages, and a backtrace, intended for submission with bug reports to Terraform support for troubleshooting.

**Enabling Verbose Logging:** In troubleshooting scenarios where standard error output lacks sufficient information, the `TF_LOG` environment variable can be set to INFO for detailed logging of Terraform's actions during `apply`. Adjusting the logging level to DEBUG or TRACE provides even more granular information. This level of logging is particularly beneficial in automated processes where human supervision is not constant.

**Key Takeaways:**

* Terraform logging can be customized by adjusting the `TF_LOG` and `TF_LOG_PATH` environment variables.
* In the event of a Terraform executable crash, a `crash.log` file is generated containing essential information for bug report submission.
* Enabling verbose logging, especially in troubleshooting situations, helps to obtain detailed information about Terraform's actions, facilitating the identification of root causes in scenarios like failed `terraform apply`.
