## **Advanced Git II: Revert, Reset, and Cherry-Pick**

### **1. Undoing Work in Git: Three Different Tools**

Every beginner eventually needs to undo something, a bad commit, a broken change, work on the wrong branch entirely. Git gives you three different tools for this, and picking the wrong one can either lose work you wanted to keep, or leave a mess you wanted gone. Understanding the difference matters more than memorizing the commands.

### **2. git revert: Undo by Adding a New Commit**

Revert undoes the changes from a specific commit, but instead of removing that commit from history, it creates a brand new commit that reverses it.

```
git revert <commit-hash>
```

Your history now shows both the original commit and the revert commit, nothing is erased, the mistake and its fix are both visible. This is the safest way to undo something, especially on a branch that's already shared with others, since it never rewrites history.

### **3. git reset: Move the Branch Pointer Backward**

Reset moves your current branch pointer back to an earlier commit. Unlike revert, it can actually rewrite history, what happens to your changes depends on which mode you use.

```
git reset --soft <commit-hash>
```
Moves the branch pointer back, but keeps all your changes staged, ready to recommit.

```
git reset --mixed <commit-hash>
```
The default mode, moves the pointer back and unstages the changes, but keeps them in your working directory as uncommitted edits.

```
git reset --hard <commit-hash>
```
Moves the pointer back and completely discards the changes, gone, not staged, not in your working directory. Use this one carefully, there's no undo for `--hard` once it's done.

### **4. Rollback: Not a Real Git Command, But a Real Concept**

You'll hear developers say "rollback" often, but it's not an actual Git command, it's the general idea of returning your project to a previous known-good state. In practice, a rollback is usually done with either `revert` (safe, adds a new commit) or `reset --hard` (rewrites history, discards changes), depending on whether the branch is shared with others or purely local.

### **5. Revert vs Reset: Which One to Use**

- Use **revert** on any commit that's already been pushed and shared, it's non-destructive and keeps a clear record
- Use **reset** only on local commits you haven't pushed yet, since it rewrites history exactly like rebase from Part 9, and the same golden rule applies: never reset shared history

### **6. git cherry-pick: Grab One Specific Commit**

Cherry-pick lets you take a single commit from one branch and apply it onto another, without merging or rebasing the entire branch.

```
git cherry-pick <commit-hash>
```

This is useful when you have one specific fix sitting on a branch you don't want to fully merge yet, a hotfix that needs to go straight to `main` without dragging in unrelated work-in-progress commits from the same branch.

### **7. Key Takeaways**

1. `git revert` undoes a commit by adding a new commit, safe for shared history since nothing is erased
2. `git reset` moves your branch pointer backward, with `--soft`, `--mixed`, and `--hard` controlling what happens to your changes, only safe on unpushed local commits
3. "Rollback" isn't a real command, it's the general idea, achieved through either revert or reset depending on context
4. `git cherry-pick` copies one specific commit onto another branch without merging everything else

---

### **Homework**

1. Make a commit, then revert it with `git revert`, and look at how both commits show up in `git log`
2. On a local test branch, try all three reset modes, `--soft`, `--mixed`, `--hard`, on a throwaway commit, and observe the difference each time with `git status`
3. Create two branches, make a commit on one, and cherry-pick just that commit onto the other
4. **Build in Public**: Post what surprised you most about reset vs revert on LinkedIn/X with #engineeringinkannada and tag me so I can see it

### **YouTube Reference**

Watch the following video from my channel:

- [Watch Part 10 on YouTube](#)

Make sure to subscribe to the channel for more tutorials and updates!