---
title: "prwatch – a utility to watch a GitHub PR's checks"
description: "a script that watches a PR's checks and sends an OS notification once all pass or if any are failing"
pubDate: "2025-06-03"
---

I created a small utility, `prwatch` – a script that takes a PR URL and watches the PR’s status checks. It sends an OS notification when a check fails or when all checks pass.

## Installation

Download the script from this Gist: https://gist.github.com/the21st/aeab60a5b4fb4e3d763f4a6762009d0f

## Usage

### Basic usage

```
prwatch <PR_URL>
```

The script will wait until either:

1. All checks are finished and reports success.
2. One check fails and reports failure.

### Option: `--all`

```
prwatch --all <PR_URL>
```

This option always waits for all checks to finish before sending a notification and terminating.
