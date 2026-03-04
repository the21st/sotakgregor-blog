---
title: "How to craft clean commits: a practical guide"
description: "A guide to clean PR commits without losing sanity."
pubDate: "2025-09-16"
---

In the [first part of this series](/blog/clean-git-commits/), I covered _why_ a clean commit history matters. Short version: it's about putting the reviewer first and telling a clear story with your code.

Now for the _how_.

I used to think editing git history meant a lot of tedious command-line `git` magic. You _could_ do all of this with `git rebase -i`. But I don't. Good tools sand down the rough edges and make the whole process fast.

I use 2 tools: **GitHub Desktop** for 90% of my daily work and **GitUp** for the trickier situations.

## The everyday workflow: GitHub Desktop

GUI is always better than CLI for git. I will die on this hill.

GitHub Desktop is my go-to for most of the committing process. It's simple, it handles the most common tasks well, and it's separate from my IDE. That last part matters. Switching to GitHub Desktop shifts my mindset from writer to reviewer. It's a mental trick: as I work on my commits, I review my own code. That self-review adds a layer of quality you don't get from going straight to `git commit`.

### Staging changes line by line

This is the foundation. I rarely make a set of changes that all belong in a single, logical commit. More often, I'll fix something in one place while bolting on a feature in another.

Instead of committing the whole file, I commit only the specific lines that belong together. In GitHub Desktop, you can uncheck entire files or specific lines you don't want to include.

So you stage and commit just the `add_new_feature()` function, leaving the unrelated change in `some_other_function()` for a separate commit.

<video controls autoplay muted loop playsinline style="max-width: 100%; border-radius: 8px;" aria-label="Demo of selecting and deselecting lines for a partial commit in GitHub Desktop">
  <source src="/assets/github-desktop-stage-lines.mp4" type="video/mp4" />
</video>

This alone will improve your commits. You start building your PR piece by piece, each commit telling one part of the story.

### Quick fixes: amending the last commit

You just pushed a commit and CI fails on linting. Or you spot a typo in a comment you just committed.

Don't create a new commit that says `"fix lint"`. Your reviewer doesn't need to see that. Edit the commit instead.

Make the change, go to the "History" tab, right-click your last commit, and choose "Amend Commit." Your fix gets folded into the previous commit as if the mistake never happened.

<video controls autoplay muted loop playsinline style="max-width: 100%; border-radius: 8px;" aria-label="Demo of amending a  commit in GitHub Desktop">
  <source src="/assets/github-desktop-amend.mp4" type="video/mp4" />
</video>

This only works for the _most recent_ commit, but it's perfect for small mistakes.

### Fixing older commits

What if you spot a mistake in a commit from 3 commits ago? That's where this killer GitHub Desktop feature comes in.

Say you've committed a bunch of clean commits that got a feature done end to end. Then you spot a bug (or CI spots it for you) in a function you added a few commits back. Here's the workflow:

1.  Make the fix in your editor.
2.  Create a new, temporary commit. The message doesn't matter. I usually just write `fixup`.
3.  Go to the History tab.
4.  Drag your `fixup` commit and drop it onto the older commit you want to fix.

GitHub Desktop squashes the 2 commits together, rewriting the history for you. It's an interactive rebase without the command line.

<video controls autoplay muted loop playsinline style="max-width: 100%; border-radius: 8px;" aria-label="Demo of squashing 2 commitsin GitHub Desktop">
  <source src="/assets/github-desktop-squash.mp4" type="video/mp4" />
</video>

If the changes conflict with a newer commit, you'll need to resolve the conflicts first. GitHub Desktop will tell you when that happens and wait for you to sort it out.

After you amend or reorder commits, you'll need to force-push. GitHub Desktop has a "Force Push Origin" button for this. I also recommend `git push --force-with-lease` from the command line, which is a safer alternative.

## Splitting commits with GitUp

Sometimes a commit has 2 distinct ideas crammed together. You added a new test for a function, but you also fixed a typo in the README in the same commit. These should be separate.

You _can_ do this with `git rebase`, but GitUp makes it much more intuitive:

1.  Open your repo in GitUp. It shows a visual graph of your commits.
2.  Find the commit you want to split.
3.  Right-click and choose "Split."
4.  GitUp shows you the diff. Select the changes (or individual lines) you want to carve out into a _new_ commit.
5.  Give the new commit a clear message.

Then force push. That's it.

<video controls autoplay muted loop playsinline style="max-width: 100%; border-radius: 8px;" aria-label="Demo of splitting a commit in GitUp">
  <source src="/assets/gitup-split-commit.mp4" type="video/mp4" />
</video>

## Red flags: how to spot a dirty PR

Before you ask for a review, scan your commit list. If you see any of these, clean up first:

- **`"fix lint"`, `"fix tests"`, `"cleanup"`** commits. Squash these into the commits that introduced the issue.
- **`"WIP"`, `"work in progress"`, `"stuff"`** commits. The clearest sign the history hasn't been tidied up.
- **A commit that refactors code added in a previous commit** _in the same PR_. The code should've been committed in its final state. Don't show your reviewer your process; show them the result.
- **A merge commit** like `Merge branch 'main' into your-feature-branch`. This clutters the history. Rebase your branch on top of `main` instead (`git rebase main`) for a clean, linear history.

## Stop editing history after review

Once someone has started reviewing your PR, stop rewriting history.

All these techniques involve force-pushing. If you do this after someone has given feedback, you'll break GitHub's review UI. Your reviewer won't be able to see what you changed in response to their comments, which creates a ton of extra work for them (exactly what we're trying to avoid).

After you get that first review, switch to adding new commits on top. You can still keep _those_ commits clean, but don't touch the ones that have already been reviewed.
