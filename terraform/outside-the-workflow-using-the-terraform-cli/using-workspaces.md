---
description: Learn when to use Terraform workspaces and their types.
---

# Using Workspaces

**When to Use Terraform Workspaces**

Think of Terraform workspaces as a handy tool, especially in big companies with various teams. It's like having different work desks for different tasks. Each team gets its own workspace, where they have the tools they need, and only they can make changes there. This way, you avoid chaos and keep things organized.

Now, imagine your company has a networking team, a governance team, and an application team. Plus, there are different environments like production, staging, and development. You can create specific workspaces for each team and environment:

* networking-dev
* networking-stage
* networking-prod
* governance-dev
* governance-stage
* governance-prod
* application-dev
* application-stage
* application-prod

This setup ensures that each team works independently, even if they share the same workspace area (like a huge office). Everyone can progress through their tasks without stepping on each other's toes. It's like having designated spaces for different projects, making collaboration smooth and organized.

And here's a cool thing – the system remembers who is working where. It's like putting name tags on the desks. So, even if multiple team members are doing their thing in different workspaces at the same time, there's no confusion. Everyone knows where they should be, and it keeps the workflow moving without any hiccups.
