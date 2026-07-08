<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Git Branching and Rebasing

**Project Link:** [View Project](https://nextwork.ai/projects/91663bbf-e290-4b23-a79a-b5ecb09d033a)

**Author:** Granada Marc Justin Lee  
**Email:** granadamarc96@gmail.com

---

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/91663bbf-e290-4b23-a79a-b5ecb09d033a_prbtm81h)

## Mastering Git for Professional Collaboration

### Project goals and motivation

In this project, I'm learning how to manage parallel branches, resolve merge conflicts manually, and use git rebase and interactive rebase to clean up commit history so that I can maintain a professional, linear, and readable Git repository while collaborating with development teams.

## Setting Up the Conflict Practice Environment

### Step overview

In this step, I'm setting up my local Cursor editor environment and initializing my Git repository with a clean working tree and starter file so that I can establish a stable, up-to-date baseline before safely practicing branch merging and conflict resolution.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/91663bbf-e290-4b23-a79a-b5ecb09d033a_41zr0tj6)

### Why create the file on main first

I created this file on the main branch so that all subsequent branches share a common ancestor and inherit the exact same starting content. This ensures that when I modify the same lines of this file differently on separate branches, Git will trigger a predictable merge conflict for me to safely practice resolving.

## Resolving a Merge Conflict

### Step overview

In this step, I'm setting up two diverging branches that edit the exact same line of a shared file so that I can intentionally trigger a merge conflict, learn how to read Git's conflict markers, and successfully resolve and push the final unified changes to GitHub.

### Understanding conflict markers

The markers show me where a merge conflict has occurred within a file. The <<<<<<< marks the start of the changes from my current local branch, often labeled as HEAD. The ======= separates my local changes from the incoming branch's changes. The >>>>>>> marks the end of the incoming changes and identifies the conflicting branch name.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/91663bbf-e290-4b23-a79a-b5ecb09d033a_n45dts6x)

## Rebasing a Feature Branch for Clean Linear History

### Step overview

In this step, I'm setting up a local feature branch with new commits and simulating teammate updates on the main branch so that I can execute a git rebase to replay my work on top of the latest changes and complete a clean fast-forward merge to maintain a linear commit history.

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/91663bbf-e290-4b23-a79a-b5ecb09d033a_wycjar4n)

### Rebase vs. merge explained

Rebasing works by moving a sequence of commits to a new base, which replays my branch changes directly on top of the target branch to create a linear commit history. While merging works by joining the histories of two branches together using a dedicated merge commit that preserves the exact historical path of how both branches evolved. I would choose git rebase when I want to clean up my local feature branch and keep the main timeline neat and easy to follow before sharing my work with others.

## Polishing Commits with Interactive Rebase

### Step overview

In this step, I'm cleaning up my disorganized feature branch commits by squashing and rewording them using an interactive rebase so that my history looks streamlined, readable, and professional with a single, clear commit before opening a Pull Request on GitHub.

### reword vs. squash commands

Reword keeps the selected commit's file changes exactly as they are but pauses the interactive rebase process to let you edit and rewrite the commit message, while squash combines both the file changes and the commit messages of one or more commits into the parent commit directly above them to condense multiple steps into a single, clean unit of work.

### Why --force-with-lease is required after rebase

I needed --force-with-lease because the interactive rebase rewrote my local commit history, causing it to diverge from the remote branch on GitHub which still held my older, messy commits. Since a standard git push blocks non-fast-forward updates to prevent accidental data loss, I had to force the update; using --force-with-lease allowed me to safely overwrite the remote history only after confirming that no one else had pushed new changes to that branch in the meantime.

## Saving Work-in-Progress with Git Stash

![Image](https://nextwork.ai/mischievous_gray_loyal_tuke/uploads/91663bbf-e290-4b23-a79a-b5ecb09d033a_otnu1qbf)

### The value of git stash in team workflows

In this project extension, I learned that git stash helps when you need to switch branches urgently to fix a teammate's bug or pull the latest updates but aren't ready to commit your unfinished work. It temporarily shelves your uncommitted changes to give you a clean working tree, allowing you to address team needs without creating messy commits or losing your progress, and safely restore your work later using git stash pop.

## Reflections and Takeaways

### Key tools and concepts

During this project, I worked extensively with tools like Git and Cursor to manage and refine my development workflow. I mastered key concepts including performing an interactive rebase to clean up history using commands like reword and squash, resolving complex merge conflicts manually, and temporarily shelving changes with git stash. Additionally, I learned how to safeguard my progress using git reflog to recover lost commits and maintain a clean, atomic commit history.

### Time and challenges

This project took me approximately 2 hours to complete. The most challenging part was managing a complex interactive rebase and dealing with a missing commit, which required using git reflog to safely recover my state. Manually identifying and resolving merge conflicts while keeping the commit history atomic also required a high level of focus and precision.

### Looking ahead

I did this project today to learn how to master advanced version control techniques, specifically executing a clean interactive rebase, manually resolving merge conflicts, and using tools like git reflog to safeguard my progress. Another skill I want to learn is how to implement automated CI/CD pipelines to integrate these branching strategies into a real-world, collaborative deployment workflow.

---

*Built with [NextWork](https://nextwork.ai) - [View this project](https://nextwork.ai/projects/91663bbf-e290-4b23-a79a-b5ecb09d033a)*
