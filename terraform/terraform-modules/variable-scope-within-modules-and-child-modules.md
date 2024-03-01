---
description: >-
  Learn the scope of local values, variables, and outputs within modules and
  child modules.
---

# Variable Scope within Modules and Child Modules

#### Making Sense of Module Configurations in Terraform

In Terraform, configuring modules involves a strategic use of inputs and outputs. Let's break down this process and understand the scope of variables, locals, and outputs in different module contexts.

#### **Understanding Module Scope**

1. **Local Values in a Module:**
   * Local values defined in a module are confined to that specific module. They don't spill over to calling modules or other child modules unless explicitly exposed as output values.
2. **Variables Within a Module:**
   * Variables have a module-wide scope. When calling a module, any variables without default values need explicit input from the calling module.
3. **Variables in Child Modules:**
   * Child modules cannot directly access variables from the calling module. Attempts like `var.naming_prefix` won't work. Information exchange requires passing variables explicitly.
4. **Local Variables in Child Modules:**
   * Similar to module variables, local variables in a child module are inaccessible to the calling module. Expressions like `local.vm_name` won't work for cross-module references.

#### **Navigating Variable and Local Scopes**

1. **Calling Module Perspective:**
   * If a calling module has a variable `naming_prefix`, attempts like `local.vm_name` or `module.virtual_machine_set.local.vm_name` won't fetch the local variable from the child module.
2. **Child Module Perspective:**
   * Similarly, if a child module has a local variable `vm_name`, references like `var.naming_prefix` or `root.var.naming_prefix` won't retrieve the variable from the calling module.

#### **Importance of Outputs**

1. **Scope of Outputs:**
   * Outputs play a crucial role in information sharing. They provide a way to pass values from one module to another.
2. **Accessing Outputs:**
   * Child modules can't directly access variables or resources in the calling module. To share information, outputs need to be defined in the child module and referenced explicitly.

#### **Practical Example: Inter-Module Communication**

In the provided example, we see how a calling module populates variables in a child module using outputs from a different module. This explicit handling of inputs and outputs ensures a clear information flow between modules.

#### **Key Takeaways:**

* **Explicit Information Sharing:** Modules need to explicitly define inputs and outputs for effective communication.
* **Scope Isolated:** Variables, locals, and outputs are scoped within their respective modules.
* **Strategic Configuration:** Understanding the scope helps in making informed decisions while configuring modules.

In summary, Terraform's module configuration relies on a precise orchestration of inputs and outputs, ensuring a modular yet interconnected infrastructure-as-code setup.
