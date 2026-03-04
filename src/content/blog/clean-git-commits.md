---
title: "The reviewer-first mindset: clean commits matter"
description: "Why writing well-structured commits is essential for productive code reviews and better teamwork."
pubDate: "2025-05-07"
---

A clean git commit history isn't about neatness or vanity. It's a tool. Clean commits lead to better, faster code reviews and fewer WTF moments when you revisit old PRs 6 months later.

I want to focus on _why_ a clean history matters, especially when you're trying to ship fast. You can read [part 2](/blog/clean-git-commits-how/) to learn _how_ to keep your commits clean.

## Examples

Here's a PR with messy commits:

```git
1: add user dashboard feature
2: fix linting
3: fix tests
4: add more tests
5: remove console.logs
6: cleanup
```

And here's the same work, structured well:

```git
1: extract user stats calculation to separate service
2: add database schema for dashboard widgets
3: implement dashboard widget API endpoints + tests
4: add dashboard UI components
```

## If it's so good, why don't we always do it?

Because it's hard work. It took me a long time to learn how to do it, and even longer to do it efficiently enough that it became a habit.

It's much easier to just `git commit -am "fix tests"` and push. It feels good to be done when all the code is there, and tidying up feels unnecessary. But skipping the cleanup usually creates more work for the team down the line.

## Better code reviews

A clean commit history strips away the noise from large PRs.

Picture this: a reviewer opens your PR and sees one massive "WIP" commit followed by scattered "fixes" and "improvements." Where do they even begin? They're forced to untangle unrelated changes while trying to reason about your overall approach.

Now picture the same reviewer opening a PR with focused commits. First, a commit that refactors a module to prepare for new functionality. Then one that introduces a new data structure. Finally, one that adds the feature on top. Each step tells a clear story. The reviewer isn't struggling to decode what happened; they're following a coherent narrative.

When each commit represents a single conceptual change, reviewers can grasp your work quickly and spend more time assessing _how well_ it was done (instead of figuring out _what_ was done).

**Don't show your reviewer all your failed experiments.** Skip the commits with failing tests and linting errors. A polished history shows the intended path to the solution, so the reviewer can focus on quality and design.

Good commit messages matter here too. A concise title summarizes the change. But the commit body can carry real weight: _why_ this approach? Were other options considered? This kind of context turns a code change into documentation.

The payoff goes beyond the immediate review. When reviewers can follow your progression step by step, they internalize the code better. Your solution becomes more memorable for everyone who touches that code later (which reduces bus factor and makes the code genuinely more maintainable).

In startups where things move fast, this means quicker feedback loops and quicker merges. Good commits that explain themselves make it much more likely you'll get a _good_ review. And good reviews are one of the best ways to grow as a developer.

## Reviewing the whole diff? You're missing out

I used to review PRs as one large diff. It felt simpler, and it was a way to avoid the messy evolution of a pull request.

That changed when I started seeing large PRs built from a series of clean commits. It was far easier to follow the developer's reasoning, which helped me give better feedback and finish reviews faster.

## Clean commits: how to move fast

Claiming "no time" for clean commits is a false economy. You're not saving time, you're pushing it onto your reviewers (with interest).

Your commits should tell the story of your solution, not document your struggle to find it.
