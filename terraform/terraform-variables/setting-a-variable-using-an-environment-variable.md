---
description: We will learn to set a variable in Terraform using an environment variable.
---

# Setting a Variable Using an Environment Variable

Another way to set variable values is by using environment variables.&#x20;

Follow these steps:

Open your terminal and set environment variables using the following convention:

*   ```bash
    export TF_VAR_bucket_name=<your-bucketname> 
    export TF_VAR_bucket_suffix=via-env
    ```

    📝 Note: Replace `<your-bucketname>` with your actual bucket name.
* After setting the environment variables, run `terraform apply`.
* Terraform will now use the values from your environment variables, and you won't be prompted for variable values during the process.

By using environment variables with the `TF_VAR_` prefix, you provide a convenient way to supply values to your Terraform variables without having to specify them in the command line or directly in your configuration files. This method enhances flexibility and security in managing your infrastructure configurations.
