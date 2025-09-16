---
title: "How to Craft Clean Commits: A Practical Guide"
description: "A guide to clean PR commits without losing sanity."
pubDate: "2025-09-16"
---

In the [first part of this series](/blog/clean-git-commits/), I talked about _why_ a clean commit history is important for faster, better code reviews. It’s about putting the reviewer first and telling a clear story with your code.

Now, let's get into the _how_.

I initially thought that editing git history means a lot of tedious command-line `git` magic. And you _could_ do all of this with `git rebase -i`. But I don't. Good tools are essential, and they can make this process fast and easy.

I primarily use two tools to keep my commit history clean: **GitHub Desktop** for 90% of my daily work and **GitUp** for the trickier situations.

## The Everyday Workflow in GitHub Desktop

The hill I'll die on is that GUI is always better than CLI.

That's why I use a GUI app to do most of my git work. GitHub Desktop is my go-to for most of the committing process. It's simple, and it handles the most frequent tasks well.

The fact that Github Desktop is separate from my IDE works to my advantage. Switching to Github Desktop changes my mindset from writer to reviewer. It's a mental trick. So as I work on my commits in Github Desktop, I review my own code. This adds a layer of quality you wouldn't get if you just went straight to `git commit`.

### The Most Important Tool: Staging Changes Line-by-line

This is the foundation. Very rarely do I make a set of changes that all belong in a single, logical commit. More often, I'll fix something in one place while adding a feature in another. Instead of committing the whole file, I commit only the specific lines that belong together.

In GitHub Desktop, you can see all your file changes. You can uncheck entire files but also specific lines that you don't want to include.

This lets you stage and commit just the `add_new_feature()` function, leaving the unrelated change in `some_other_function()` to be committed separately.

<video controls autoplay muted loop playsinline style="max-width: 100%; border-radius: 8px;" aria-label="Demo of selecting and deselecting lines for a partial commit in GitHub Desktop">
  <source src="/assets/github-desktop-stage-lines.mp4" type="video/mp4" />
</video>

Using this will already improve your commits. You start building your PR piece by piece, with each commit telling one part of the story.

### Quick Fixes: Amending the Last Commit

You just pushed a commit, and the CI fails because of linting violations. Or you notice a typo in a code comment you just committed.

Don't create a new commit that says `"fix lint"`. Your reviewer doesn't need to see that mistake. Edit the commit instead.

Make the change, go to the "History" tab in GitHub Desktop, right-click your last commit, and choose "Amend Commit." Your new changes will be rolled into the previous commit as if you'd never made the mistake.

<video controls autoplay muted loop playsinline style="max-width: 100%; border-radius: 8px;" aria-label="Demo of amending a  commit in GitHub Desktop">
  <source src="/assets/github-desktop-amend.mp4" type="video/mp4" />
</video>

You can only do this for the _most recent_ commit, but it's perfect for quick fixes of small mistakes.

### Fixing Older Commits

What if you spot a mistake in a commit you made three commits ago? That's where this killer GitHub Desktop feature comes in.

Let's say you've committed a bunch of clean commits that got a feature done end-to-end. And then you spot a mistake or CI tells you about an issue in a function you added a few commits back. Here’s the workflow:

1.  **Make the fix** in your editor.
2.  **Create a new, temporary commit.** The message doesn't matter. I often use something like `fixup`.
3.  Go to the **History tab**.
4.  **Drag your new `fixup` commit and drop it directly onto the older commit** you want to fix.

GitHub Desktop will ask you to confirm, and then it will squash the two commits together, rewriting the history for you. It's an interactive rebase, but without the command-line.

<video controls autoplay muted loop playsinline style="max-width: 100%; border-radius: 8px;" aria-label="Demo of squashing 2 commitsin GitHub Desktop">
  <source src="/assets/github-desktop-squash.mp4" type="video/mp4" />
</video>

If the changes in your `fixup` commits conflict with one of the newer commits, you'll need to resolve the conflicts before you can continue. Don't worry – Github Desktop will tell you when there are conflicts and will wait for you to resolve them.

After you amend or reorder commits, you'll need to force-push your changes. GitHub Desktop has a "Force Push Origin" button that makes this easy. I also recommend using `git push --force-with-lease` from the command line, as it's a safer way to force-push.

## For Heavy-Duty Work: Splitting Commits with GitUp

Sometimes a commit contains two or more distinct ideas. For example, you add a new test for a function, but in the same commit, you also fix a typo in the README. These should be separate.

While you _can_ do this with `git rebase`, GitUp makes it much more intuitive.

1.  Open your repo in GitUp. It shows you a visual graph of your commits.
2.  Find the commit you want to split.
3.  Right-click on it and choose "Split".
4.  GitUp will show you a diff. You can select the changes (or even individual lines) that you want to move into a _new_ commit.
5.  Give your new commit a clear message.

And then, don't forget to force push. That's it!

<video controls autoplay muted loop playsinline style="max-width: 100%; border-radius: 8px;" aria-label="Demo of splitting a commit in GitUp">
  <source src="/assets/gitup-split-commit.mp4" type="video/mp4" />
</video>

## Red Flags: How to Spot a "Dirty" PR

Before you ask for a review, give your own commit list a quick scan. If you see any of the following, it’s a sign that you should do some cleanup first.

- Any commit with a message like `"fix lint"`, `"fix tests"`, or `"cleanup"`. These changes should be squashed into the commits that introduced the issue.
- Commits named `"WIP"`, `"work in progress"`, or `"stuff"`. This is the clearest sign that the history hasn't been tidied up.
- A commit that refactors or moves code that was just added in a previous commit _in the same PR_. The code should have been committed in its final, refactored state to begin with. Don't show your reviewer your process – show them the polished result.
- A merge commit. Usually its summary is `Merge branch 'main' into your-feature-branch`. This clutters the history. Instead of merging `main` into your branch, you should **rebase** your branch on top of `main` (`git rebase main`). This creates a clean, linear history that's much easier to follow.

## The Caveat: Stop Editing History After Review

**Once a human has started reviewing your PR, stop rewriting history.**

All the techniques above involve force-pushing, which rewrites the commit history. If you do this after someone has given you feedback, you'll break GitHub's review UI. Your reviewer won't be able to easily see what you changed in response to their comments, creating a ton of extra work for them. And that's exactly what we're trying to avoid!

After you get that first review, switch to adding new commits on top to address the feedback. You can still keep _those_ new commits clean, but don't touch the ones that have already been reviewed.

---

It takes a little practice, but crafting clean commits quickly becomes a habit. It's a small investment of your time that has a huge payoff in the speed and quality of your code reviews. Give it a try!
