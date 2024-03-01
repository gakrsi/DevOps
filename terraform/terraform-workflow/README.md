---
description: Learn about Terraform's core workflow.
---

# Terraform Workflow

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

#### Navigating the Terraform Workflow: Write, Plan, Apply

**Write: Crafting Infrastructure as Code (IaC)**

In the initial phase of the Terraform workflow, crafting infrastructure is akin to traditional coding. Utilizing integrated development environments (IDEs) or advanced text editors, we author our IaC. HashiCorp Configuration Language (HCL) or JSON serves as the coding language, with HCL being the preferred choice due to its human-friendly nature. Source control management (SCM) becomes a best practice, offering versioning and change tracking. The process thrives on consistent code validation to catch syntax errors early on.

**Plan: Visualizing Changes Before Implementation**

Moving forward, the planning stage acts as a critical checkpoint. Here, we evaluate the anticipated changes in the target environment. Even with a clear end goal, planning helps validate our assumptions against the reality of Terraform's actions. Continuous validation, often through incremental changes and frequent use of `terraform plan`, safeguards against major troubleshooting later on. The option to save proposed plans to a file provides an additional layer of review before the actual application.

**Apply: Bringing Configurations to Life**

The culmination of the Terraform journey lies in the application phase. Applying the updated configuration to the target environment brings our IaC to life. Post-successful application, committing changes to source control ensures their persistence and guards against inadvertent loss. This cyclical workflow aligns with the dynamic nature of infrastructure requirements, emphasizing continuous improvement.

**Reiterate: Embracing Continuous Improvement**

As the deployment concludes, we embark on a new cycle. The iterative nature of infrastructure needs demands a constant loop of configuration adjustments, planning, and application. Each phase informs the next, aligning Terraform practices with the principles of an ever-evolving software development lifecycle.

**Key Takeaways:**

* **Fluid Workflow:** Terraform's workflow flows seamlessly through the triad of write, plan, and apply stages.
* **Vigilant Planning:** Regular planning avoids pitfalls, ensuring configurations align with expectations.
* **Continuous Improvement:** The cyclical nature of the process acknowledges the evolving landscape of infrastructure requirements.

In essence, Terraform's workflow encapsulates a pragmatic approach to infrastructure management, balancing planning precision with the agility to adapt to changing needs.
