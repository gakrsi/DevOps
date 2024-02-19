---
description: We will learn how to set variables in Terraform using a file.
---

# Setting a Variable Using a File

Another method to set variable values is by using a file, specifically named `terraform.tfvars`. Follow these steps:

**Create `terraform.tfvars` File:**

* In your project, create a new file named `terraform.tfvars`.
*   Inside this file, provide values for the variables using the format:

    ```hcl
    bucket_name = "<your-bucketname>" bucket_suffix = "from-file"
    ```

    📝 Note: Replace `<your-bucketname>` with your chosen bucket name.
* Save the `terraform.tfvars` file.
* Now, when you run the project using `terraform apply`, Terraform will automatically use the values from the `terraform.tfvars` file for the specified variables.

📝 Note: Ensure that the `terraform.tfvars` file is in the same directory as your Terraform configuration files.

#### Another File Naming Option

Alternatively, you can use any file name ending with `.auto.tfvars`. Terraform recognizes files with this ending and considers them for variable values. You can even define multiple files, each containing values for different variables.

By using a file for variable values, you simplify the process of providing inputs to your Terraform project. It's a clean and organized way to manage configuration, especially when dealing with multiple variables or different environments.
