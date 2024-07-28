---
description: Explore the fundamentals of Git.
---

# Git Basic

his chapter covers the following essential Git commands:

* **`git init`**
* **The `.git` folder**
* **`git log`**
* **`git status`**
* **`git add`**
* **`git commit`**
* **`git diff`**

These tools are crucial as they form the core operations you'll frequently use in Git.



#### Initializing a Git Repository

To start using Git for your project, follow these steps:

1. **Initialize the Repository:**
   * Run `git init` in the root folder of your project.
   * This creates a `.git` folder, where your entire repository is stored.

* **HEAD File:**
  * The `HEAD` file is crucial because it points to the current branch or commit ID you are on.
  * You can view its contents with: `cat HEAD`.
  * It typically contains: `refs/heads/master`, indicating the default master branch.
* **Config File:**
  * The `config` file holds your repository’s local configuration, such as branch and remote repository information.

Notes

* There are global Git configuration files on your host system, but you can ignore them for now.
* Detailed exploration of all files in the `.git` folder is beyond this course's scope, but you will learn about some of them as you progress.
