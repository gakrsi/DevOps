# Introduction to Git

### The Four Phases of Git Content

In Git, your code moves through four distinct phases. Grasping these four stages is essential for mastering Git.

At first, this might seem overly complex, but as you become more familiar with Git, it will make more sense. If you've ever found Git confusing, it's probably because these stages weren't fully understood. While you can use Git without a deep knowledge of its workings, eventually, you'll need a better understanding to tackle more complex tasks.

<div data-full-width="false">

<figure><img src="../.gitbook/assets/6465f5b7125e4_what_is_git_1.jpg" alt=""><figcaption><p>The four phases of Git content</p></figcaption></figure>

</div>

### How Git Differs from Other Version Control Systems (VCSs)

**History is more malleable**

* You can alter the history in your repository and in others' (with the right permissions).

**Branching is cheap**

* Branching in traditional VCSs (like CVS and Subversion) is slow and depends on the number of files (O(n)).
* In Git, branching is quick and independent of repository size (O(1)).
* This makes it easier to experiment with branches and delete them when no longer needed.

**Commits are made across the whole project**

* Changes in Git are applied across the entire project, not just individual files.
* This means moving or renaming files retains their history, unlike in file-oriented systems like CVS.

**No version numbers**

* Git does not use version numbers. Instead, it assigns a unique hash to each commit.
* These hashes are used to refer to changes in the repository.

