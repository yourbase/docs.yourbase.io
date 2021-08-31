---
layout: default
title: Troubleshooting
nav_order: 9
permalink: /troubleshooting
---

# Troubleshooting errors
{: .no_toc }

This is a list of commonly encountered problems, known issues, and their solutions.

## Topics
{: .no_toc .text-delta }

- TOC
{:toc}

## Build failure due to reduced code coverage
YourBase Test Acceleration is designed to avoid test runs that do not need to be executed. The percentage covered may appear lower than what is actually covered as a result. If your CI is configured to fail a build based on the percentage covered, you may need to reconfigure this feature, or check if YourBase Test Acceleration supports [filling of missing coverage data with data from previous runs on your code coverage tool](advanced-usage/integrate-code-coverage-tools.md).

---

## Unittest setUp or tearDown overrides lead to incorrect test skipping

If you are using [unittest](https://docs.python.org/3/library/unittest.html) and define your own `setUp` or `tearDown` functions, be sure they call `super` before performing other actions:

```python
class MyTestClass:
   def setUp(self):
      super(self.__class__, self).setUp()
      # ...

   def tearDown(self):
      super(self.__class__, self).tearDown()
      # ...
```

If you are not defining your own `setUp` and `tearDown` functions, you don't need to do this.

---

## __Sqlite3 module not found
If you run into errors about the _sqlite3 module not being found, follow the below steps:

1. Install <a href="https://www.sqlite.org/quickstart.html">sqlite3</a>

2. Rebuild and reinstall the Python version you are using. If you use [pyenv](https://github.com/pyenv/pyenv), this will look something like:

```sh
pyenv install --force <PYTHON_VERSION>
```

If the above step doesn't work, try:
```sh
PYTHON_CONFIGURE_OPTS="--enable-loadable-sqlite-extensions"
pyenv install --force <PYTHON_VERSION>
```

---

## Incompatibility with Apple machines having the M1 chip

YourBase Test Acceleration doesn't currently support Apple machines running the M1 chip. This is on our roadmap. If this is causing an issue for you, please reach out to us at [support@yourbase.io](mailto:support@yourbase.io).

---

## Conflict with proxy objects

Python objects that opaquely wrap other objects by overriding Python builtins like `name` and `class` can cause tracing issues in YourBase Test Acceleration that may manifest as errors from within those proxy objects. If you experience these issues, you can set to use a slower tracing algorithm that should avoid these errors. 

```sh
export YOURBASE_TIMID=true
```

_Note that this since flag dramatically increases the tracing overhead, so we don't recommend setting this if you are not experiencing issues._

---

## Conflict with plugin pytest-xdist

YourBase Test Acceleration and [pytest-xdist](https://pypi.org/project/pytest-xdist/) plugins have similar goals, reducing the overall test execution time of tests, but take different approaches to solving the problem. When they're both enabled, there are conflicts. When you're using YourBase Test Acceleration, please uninstall [pytest-xdist](https://pypi.org/project/pytest-xdist/) or execute pytest-xdist with `NUMCPUS=0`.
