---
layout: default
title: Accelerate tests in CI
nav_order: 4
parent: Advanced usage
permalink: /advanced-usage/accelerate-tests-in-ci
---

# Integrate with CI
YourBase Test Acceleration uses a [dependency
graph](../how-it-works.md#dependency-graph) to accelerate your tests. When you run tests
on your local machine with YourBase Test Acceleration enabled, by default your
dependency graph is stored locally and cannot benefit runs on other machines.

The true power of YourBase Test Acceleration shows when tests can be accelerated in your
CI environment. This requires that a [dependency
graph](../how-it-works.md#dependency-graph) be accessible by your CI environment even
when the environment is constantly torn down and rebuilt. We call this a [shared
dependency graph](../how-it-works.md#shared-dependency-graph).

On this page, you'll learn how to accelerate tests in CI using a shared dependency
graph.

## Steps to integrate with CI

### Step 1: Set up a shared dependency graph
YourBase Test Acceleration supports storing [shared dependency
graphs](../how-it-works.md#shared-dependency-graph) only in AWS S3 buckets.

1.  Set [`YOURBASE_REMOTE_CACHE`](../environment-variables.md#yourbase_remote_cache) in
    your environment to a valid S3 bucket location.

    ```sh
    YOURBASE_REMOTE_CACHE=s3://<bucketname>[/key/prefix]

    # e.g.
    YOURBASE_REMOTE_CACHE=s3://mycompany-build-artifacts/ci
    ```

    YourBase will store its artifacts in a `/yourbase` "directory" inside the path you
    specify.

2. Set the AWS credentials to be used by YourBase Test Acceleration. YourBase requires
   these permissions to use your bucket:
   ```
   s3:GetObject
   s3:PutObject
   s3:DeleteObjects
   s3:ListObjects
   s3:ListObjectsV2
   ```

   By default, your [system credentials][aws-system-credentials] are used. If you mock
   your system credentials for your test suite, you may need to specify non-mocked
   credentials exclusively for YourBase. You can do this by setting
   [`YOURBASE_AWS_ACCESS_KEY_ID`][YOURBASE_AWS_ACCESS_KEY_ID] and
   [`YOURBASE_AWS_SECRET_ACCESS_KEY`][YOURBASE_AWS_SECRET_ACCESS_KEY].

   [aws-system-credentials]:
   https://docs.aws.amazon.com/cli/latest/userguide/cli-configure-files.html
   [YOURBASE_AWS_ACCESS_KEY_ID]: ../environment-variables.md#yourbase_aws_access_key_id
   [YOURBASE_AWS_SECRET_ACCESS_KEY]: ../environment-variables.md#yourbase_aws_secret_access_key

### Step 2: Install YourBase Test Acceleration in your CI environment
Add YourBase Test Acceleration to your project according to the [instructions for your
language and testing framework][install-yourbase].

[install-yourbase]: ../getting-started

### Step 3: Run tests
Run tests as usual.

## That's it!
The above steps will set up YourBase Test Acceleration to synchronize dependency graphs
to the specified storage location when your tests run on your CI environment. Future
runs will use the storage location as the source for their dependency graph,
accelerating runs even when the environment is brand new.

_Note:_
_A dependency graph is synchronized with the specified remote storage location:_
- _Only when it's generated from a successful build, and_
- _Only if it's created from a clean working tree, and_
- _Only if it's created from committed code changes. A dependency graph that is created from uncommitted code changes is stored only locally, i.e., it can’t be synchronized against a remote location._
