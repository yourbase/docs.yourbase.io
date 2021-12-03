---
layout: default
title: unittest
nav_order: 2
parent: Getting started
permalink: /getting-started/unittest
---

# unittest + YourBase
{:.no_toc}

On this page you'll learn how to accelerate your [unittest][unittest] tests with
YourBase. For a more in-depth acceleration walkthrough using a sample project, see [our
pytest page](pytest.md).

[unittest]: https://docs.python.org/3/library/unittest.html

Table of contents
{: .text-delta }

1. TOC
{:toc}

---

## Prerequisites
- Make sure tests are running successfully with unittest before installing YourBase.
- [Install YourBase][install].
- Your project must use Git and must have at least one commit. Git must be installed.
- Your Git workspace should be clean.

[install]: ../install.md


## Enable acceleration for your project

### Step 1: Attach yourbase to unittest
{:.no_toc}

In your `tests/__init__.py file`, copy-paste the following:

```python
import unittest
import yourbase

yourbase.attach(unittest)
```

### Step 2: Run your project’s tests
{:.no_toc}
[step-2]: #step-2-run-your-projects-tests

For example, to run all the tests for the project, use:
```sh
python -m unittest discover
```

_Note: If your tests are going to take a while to run, you can run just a subset of your
tests. Running a subset of tests will create a dependency graph just for those tests, so
you can see YourBase Test Acceleration in action more quickly._


### Step 3: Re-run your tests
{:.no_toc}

Without making a code change, run your tests again using the same command as in [step
2][step-2].

You'll see that no tests are run. Since no code was changed since the last test run,
YourBase Test acceleration ensures that no tests are run.

### Step 4: Make a code change that would affect a test
{:.no_toc}

We've seen that YourBase can skip tests when they're not affected by code changes. Let's
now see that it can run tests when they are!

Make a change to a function that gets called (directly or indirectly) by one or more
tests. The change can be as simple as adding a print statement like:

```python
print("Checking YourBase Test Acceleration after a code change...")
``` 


### Step 5: Run your tests again
{:.no_toc}

Use the same command as in [step 1][step-1] to run your tests. Here, YourBase Test
acceleration ensures the tests that depend on the changed function run, and others
don't.
