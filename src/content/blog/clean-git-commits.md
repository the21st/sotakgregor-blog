---
title: "The reviewer-first mindset: clean commits matter"
description: "Why writing well-structured commits is essential for productive code reviews and better teamwork."
pubDate: "2025-05-07"
---

A clean git commit history isn't about neatness or vanity. Clean commits are a tool that leads to better and faster code reviews, and fewer WTF moments when you come back to old PRs. While mastering all the git tricks can take time, here I want to focus on _why_ a clean history within a pull request is so valuable, especially when you're trying to build things quickly.

I'll write about _how_ to keep your commits clean in an upcoming post.

## Examples

To set the stage, here's an example of a PR with messy commits:

```git
1: add user dashboard feature
2: fix linting
3: fix tests
4: add more tests
5: remove console.logs
6: cleanup
```

And here's what a well-structured PR might look like:

```git
1: extract user stats calculation to separate service
2: add database schema for dashboard widgets
3: implement dashboard widget API endpoints + tests
4: add dashboard UI components
```

## If it's so good, why don't we always do it?

If clean commits are so obviously beneficial, why aren't our git logs always clean? Building a PR with clean commits is hard work. It took me a long time and effort to learn how to do it, and then even more time to do it efficiently and make a habit of it. It's much simpler to just `git commit -am "fix tests"` and push. It feels good to be done with a pull request when all the code is there, and and tidying up can feel unnecessary. But not cleaning up often creates more work and confusion for the team down the line.

## Better code reviews

A clean commit history simplifies reviews of large pull requests. A lot. Picture this: a reviewer opens your PR and sees one massive "WIP" commit followed by a series of scattered "fixes" and "improvements." Where do they even begin? They're forced to untangle various unrelated changes, trying to decode a jumble of edits while reasoning about your overall approach.

Now imagine that same reviewer opening a PR with a sequence of focused commits. First, a commit that refactors a specific module to prepare for new functionality. Then a commit that introduces a new data structure. Finally, a commit that adds the new feature, building on the earlier refactoring and data prep. Each step tells a clear story. The reviewer isn't struggling to understand what happened – they're following a coherent narrative of development.

This is the power of well-scoped, logically organized commits. When each commit represents a single conceptual change, reviewers can grasp your changes quickly and follow the thinking behind your solution. They spend less time figuring out what changed and more time assessing how well it was done.

_Don't waste your reviewer's time by showing them all your failed experiments._ Skip the initial commits with failing tests and linting errors. A polished commit history shows the intended path to the final solution, allowing the reviewer to concentrate on the quality and design of that solution rather than being distracted by the messy intermediate process.

Good commit messages are crucial here. A concise title summarizes the change, but the commit description can carry more weight. For important changes, it should explain the 'why' behind the change. Why was this approach taken? Were other options considered? What are the implications? This context transforms a simple code change from a snapshot in time into a piece of documentation.

The benefits extend far beyond the immediate review. When reviewers can follow your logical progression step-by-step, they internalize the code better. This makes your solution more memorable – not just for you, but for everyone who touches that code later. This reduces bus factor and makes the code genuinely more maintainable.

Especially in startups where things move fast, this efficiency boost means faster feedback loops and quicker merges. _Good commits that explain themselves make it much more likely for you to get a good review!_ And good reviews are one of the best opportunities to grow as a developer.

## Reviewing the whole diff? You're missing out

I used to prefer reviewing all changes in a pull request as one large diff; it felt straightforward and it was a way to avoid seeing the messy evolution of a pull request. That changed when I started seeing large pull requests built from a series of clean commits. The difference was obvious: it was far easier to follow the developer's reasoning, which in turn helped me give better feedback and complete reviews more quickly.

## Clean commits: it's how to move fast

Claiming 'no time' for clean commits is often a false economy. You're not saving time – you're deferring it, with interest, onto your reviewers. Your commits should tell the story of your solution, not document your struggle to find it.
