## **Git Worktrees**

### **1. The Problem: One Folder, One Branch at a Time**

So far, your repository has had one working folder, and that folder shows exactly one branch at a time. When you switch branches, Git rewrites the files in that folder to match. That works fine until the day you're halfway through a feature and an urgent bug lands on your plate.

You have two options from earlier parts. You can commit half-finished work just to get out of the way, or you can stash it (Part 9), switch branches, fix the bug, switch back, and pop the stash. Both work, but both are friction, and both carry a small risk of losing track of what was in progress.

### **2. What is a Git Worktree?**

A worktree is an additional working folder linked to the same repository. Each worktree has its own branch checked out and its own files on disk, but they all share one underlying Git history.

Think of it like having two desks in the same office. Same filing cabinet (the repository history), but each desk has its own work spread out on it. You never have to clear one desk to start working at the other.

Your original folder is called the **main worktree**. Any extra folders you create are called **linked worktrees**.

### **3. Creating a Worktree**

To check out an existing branch into a new folder:

```
git worktree add ../hotfix-folder hotfix-branch
```

To create a brand new branch and its folder in one step:

```
git worktree add -b fix-login ../fix-login-folder
```

The path you give is where the new folder gets created. It's common to place it next to your main project folder rather than inside it, so the two don't get tangled up.

### **4. Listing Your Worktrees**

```
git worktree list
```

This shows every worktree attached to the repository, along with the folder path, the commit it's on, and the branch checked out there. It's the quickest way to see what you have open.

### **5. Working Inside a Worktree**

Open the new folder and everything behaves like a normal repository. You can edit files, stage, commit, and push from there. Commits made in any worktree are immediately visible to the others, since they all share the same history.

You can also open each worktree in its own VS Code window, so you can see both branches side by side without switching anything.

### **6. The One Rule: A Branch Can Only Live in One Worktree**

Git won't let you check out the same branch in two worktrees at the same time. If you try, it stops with an error. This is a safety feature, since two folders editing the same branch would quickly lead to confusion over which one is the real, current version.

If you need to look at the same code twice, create a new branch from it, or check out a specific commit in detached mode.

### **7. Removing a Worktree**

When you're done, remove the worktree cleanly:

```
git worktree remove ../hotfix-folder
```

This deletes the folder and unlinks it from the repository. Your commits are safe, because they live in the shared history, not in that folder. If you ever delete a worktree folder by hand instead, clean up the leftover record with:

```
git worktree prune
```

Git will refuse to remove a worktree that has uncommitted changes unless you force it, which protects you from deleting unsaved work by accident.

### **8. When Worktrees Are Useful**

- **Urgent hotfix mid-feature**: fix the bug in a second folder without disturbing your unfinished work
- **Reviewing a PR locally**: check out the contributor's branch in its own folder and run it, while your own work stays untouched
- **Comparing two branches**: keep both open side by side and run them at the same time
- **Long-running tasks**: run tests or a build on one branch while you keep coding on another
- **Parallel work with AI coding tools**: give each agent its own worktree so they never overwrite each other's files

### **9. Worktree vs Stash vs Clone**

- **Stash** is a temporary shelf. Good for a quick switch, but your work is hidden and easy to forget about.
- **A second clone** gives you a separate folder too, but it duplicates the whole history on disk and has to be kept in sync separately.
- **A worktree** gives you a separate folder with no duplicate history, and every commit shows up everywhere instantly.

### **10. Things to Watch Out For**

Each worktree is its own folder, so anything that isn't tracked by Git is not shared between them. That includes installed dependencies like `node_modules` or a Python virtual environment, `.env` files, and build output. You'll need to set these up again in each new worktree.

### **11. Key Takeaways**

1. A worktree is an extra working folder linked to the same repository, with its own branch checked out
2. `git worktree add` creates one, `git worktree list` shows them, and `git worktree remove` cleans one up
3. A branch can only be checked out in one worktree at a time
4. Worktrees remove the need to stash or commit half-done work just to switch tasks
5. Untracked files like dependencies and `.env` are not shared, so each worktree needs its own setup

---

### **Homework**

1. In your practice repository, create a worktree for a new branch using `git worktree add -b`, make a commit inside it, and check that the commit shows up from your main folder with `git log`
2. Try to check out the same branch in two worktrees and read the error Git gives you
3. Remove the worktree with `git worktree remove` and confirm it's gone with `git worktree list`
4. **Build in Public**: Post a screenshot of two VS Code windows open on two worktrees on LinkedIn/X with #engineeringinkannada and tag me so I can see it

### **YouTube Reference**

Watch the following video from my channel:

- [Watch Part 11 on YouTube](#)

Make sure to subscribe to the channel for more tutorials and updates!