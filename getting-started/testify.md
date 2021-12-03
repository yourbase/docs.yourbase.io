---
layout: default
title: Testify
nav_order: 3
parent: Getting started
permalink: /getting-started/testify
---

# Testify + YourBase
{:.no_toc}

On this page you'll learn how to accelerate your [Testify][testify] tests with YourBase.
For a more in-depth acceleration walkthrough using a sample project, see [our pytest
page](pytest.md).

[testify]: https://github.com/yelp/testify

Table of contents
{: .text-delta }

1. TOC
{:toc}

---

## Prerequisites
- Make sure tests are running successfully with Testify before installing YourBase.
- [Install YourBase][install].
- Your project must use Git and must have at least one commit. Git must be installed.
- Your Git workspace should be clean.

[install]: ../install.md

## Enable acceleration for your project

### Step 1: Run your project's tests with the wrapped Testify CLI
{:.no_toc}
[step-1]: #step-1-run-your-projects-tests-with-the-wrapped-testify-cli

YourBase supplies a wrapper for the Testify command-line tool that serves as a drop-in
replacement which applies acceleration.

_Note: If your tests are going to take a while to run, you can run just a subset of your
tests. Running a subset of tests will create a dependency graph just for those tests, so
you can see YourBase Test Acceleration in action more quickly._

To use it, replace invocations of `testify` with `yourbase testify`:

```sh
# Old
testify <files ...>

# New
yourbase testify <files ...>
```

#### Using with Coverage.py
{:.no_toc}

If you use use Testify with Coverage.py, instead replace the command like so:

```sh
# Old
coverage run -m testify.test_program <files ...>

# New
coverage run -m yourbase.plugins.testify <files ...>
```

### Step 2: Re-run your project's tests
{:.no_toc}

Without making a code change, run your tests again using the same command as in [step
1][step-1].

You'll see that no tests are run. Since no code was changed since the last test run,
YourBase Test acceleration ensures that no tests are run.

_Note: When Testify runs no tests, it may exit nonzero and use the word "ERROR" to
describe the results. This is normal Testify behavior, but the `yourbase` wrapper will
override it in a future update._

### Step 3: Make a code change that would affect a test
{:.no_toc}

We've seen that YourBase can skip tests when they're not affected by code changes. Let's
now see that it can run tests when they are!

Make a change to a function that gets called (directly or indirectly) by one or more
tests. The change can be as simple as adding a print statement like:

```python
print("Checking YourBase Test Acceleration after a code change...")
``` 


### Step 4: Run your tests again
{:.no_toc}

Use the same command as in [step 1][step-1] to run your tests. Here, YourBase Test
acceleration ensures the tests that depend on the changed function run, and others
don't.
