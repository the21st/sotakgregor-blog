---
title: "The reviewer-first mindset: clean commits matter"
description: "The reviewer-first mindset: clean commits matter"
pubDate: "2025-05-07"
---

A clean git commit history isn't about neatness or vanity. Clean commits are a tool that leads to better and faster code reviews, and fewer WTF moments when you come back to old PRs. While mastering all the git tricks can take time, here I want to focus on _why_ a clean history within a pull request is so valuable, especially when you're trying to build things quickly.

## If it's so good, why don't we always do it?

If clean commits are so obviously beneficial, why aren't our git logs always clean? Building a PR with clean commits is hard work. It took me a long time and effort to learn how to do it, and then even more time to do it efficiently and make a habit of it. It's much simpler to just `git commit -am "fix tests"` and push. It feels good to be done with a pull request when all the code is there, and and tidying up can feel unnecessary. But not cleaning up often creates more work and confusion for the team down the line.

## Better code reviews

A clean commit history simplifies reviews of large pull requests. A lot. When commits are well-scoped and logically organized, reviewers can grasp your changes quickly and provide more useful feedback.

When each commit is a single conceptual change, reviewers can follow the thinking behind your solution. Consider the difference: A reviewer faced with one large initial WIP commit and several subsequent smaller "fixes" and "improvements" commits has to reason about various unrelated changes. It's hard to know where to begin.

Now, imagine that same set of changes presented as a sequence of focused commits: first, perhaps, a commit that refactors a specific module to prepare for new functionality. Then a commit that introduces a new data structure. Finally, a commit that adds the new feature, building on the earlier refactoring and data prep. Each step is clear. The reviewer isn't struggling to decode a jumble of edits; they're following a coherent story of development.

_Don't waste your reviewer's time by showing them all your failed experiments_, like an initial commit with failing tests and linting errors. A polished commit history shows the intended path to the final solution. This allows the reviewer to concentrate on the quality and design of that solution, rather than being distracted by the intermediate, sometimes messy, process of its creation.

Good commit messages are crucial here. A concise title is a summary, but the commit description often carries more weight. It should explain the 'why' behind the change. Why was this approach taken? Were other options considered? What are the implications? This context transforms a simple code change from a snapshot in time into a piece of documentation.

Well-structured commits mean reviewers spend less time figuring out what changed and more time assessing how well it was done. Especially in startups, every day counts, and this efficiency boost means faster feedback loops and quicker merges.

_Good commits that explain themselves make it much more likely for you to get a good review!_ Good reviews are the best opportunity to grow as a developer.

## Reviewing the whole diff? You're missing out

I used to prefer reviewing all changes in a pull request as one large diff; it felt straightforward and it was a way to avoid seeing the messy evolution of a pull request. That changed when I started seeing large pull requests built from a series of clean commits. The difference was immediate: it was far easier to follow the developer's reasoning, which in turn helped me give better feedback and complete reviews more quickly.

## What about small pull requests?

If your entire pull request addresses one small, logical change, then it makes sense to squash any intermediate "work-in-progress" commits into a single, clear commit before requesting a review. There's little value in making reviewers trace tiny, incremental steps if the outcome is one self-contained update.

## Clean commits: it's how to move fast

Claiming 'no time' for clean commits is often a false economy. You're not saving time – you're deferring it, with interest, onto your reviewers. Don't just write code, write a narrative.
