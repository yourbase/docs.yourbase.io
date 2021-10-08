---
layout: default
title: Releases
nav_order: 10
has_children: false
permalink: /releases
---

# Release history

## Python

- 7.0.8 (2021-10-06)
  - Fixed a bug with relative path for tests
- 7.0.7 (2021-10-04)
  - Removed our copy of `asttokens`
  - Collect trace information for file being parsed
- 7.0.6 (2021-10-04)
  - Fix a crash when a function was defined beneath an `if`
- 7.0.5 (2021-10-01)
  - Change to AST-based function graph for correctness and reliability
- 6.0.7 (2021-08-10)
  - Adds extra output to Git initialization errors
- 6.0.6 (2021-08-09)
  - Fixes a bug where certain types of pytest tests can cause a fatal error
- 6.0.5 (2021-08-06)
  - Fixes a `KeyError` coming from inside Coverage.py
- 6.0.4 (2021-08-04)
  - Fixes a possible race condition with writing Coverage.py data to disk
  - Adds cohorting support for `unittest` users
  - Fixes an acceleration issue when tests are not in a Python package
- 6.0.3 (2021-07-29)
  - Fixes a regression in line tracing correctness
  - Adds additional debug output
- 6.0.2 (2021-07-20)
  - Fixes a regression in v6.x stable which causes remote dependency graphs to never be used
- 6.0.0 (2021-07-15)
  - Switched to line-level tracing
    - Comment-only changes do not trigger test re-runs
    - Changes to un-entered if statements or other branching blocks do not trigger test re-runs
    - Tests that trigger early function returns are not re-run if code after the early return changes
  - Polish
    - Major performance improvements—Boot time, shutdown time, and tracing overhead have all been significantly improved over v5.x.
    - Improved graph selection algorithm—Git history on the local machine is now utilized more efficiently to select a dependency graph that's more similar to the current project state, meaning on average fewer tests need to run.
    - Improved compatibility with Coverage.py—No more reports of 10% coverage because YourBase skipped 90% of your tests 😜 Coverage data is now included in the dependency graph and inherited by accelerated runs for skipped tests.
      - Note: 6.x requires Coverage.py 5.5+. If you depend on Coverage.py's reports programmatically, you must set run.relative_files = true in your .coveragerc. See [YourBase Documentation](https://pypi.org/project/yourbase) for details.
    - Added yourbase CLI—Gain insights about your code, powered by the dependency graph! yourbase get-affected-tests will return JSON of each test that's been affected by the current change set. More dev-friendly insights to come!
    - Dynamically change cohort count—When the total number of test cohorts changes, acceleration will Do The Right Thing and reshuffle cached data without needing a cold build.
    - Improved debug output—when running with YOURBASE_DEBUG=true, timing metrics and detailed collection information is now displayed.
  - Minor improvements, notes, and bug fixes:
    - When YOURBASE_IGNORE_LOCAL_CACHE=true is set, the local cache is neither read from nor written to (changed from: not read from, but still written to).
    - When no Git repository is present, an error is printed, YourBase self-disables, and test continue (changed from: an error is printed and the process is stopped).
    - When YOURBASE_DISABLE=true is set, YourBase is disabled before it bootstraps itself, fixing some issues with initialization or configuration issues failing builds even with YourBase disabled.
    - When running your tests with a debugger, YourBase self-disables automatically. This helps avoid confusion when YourBase skips some code containing a breakpoint.
- 5.2.4 (2021-06-04)
  - Adds a temporary workaround to a `pytest` behavior that causes skipped tests' teardown hooks to be run even when their corresponding setup hooks weren't; all setup and teardown hooks will now be run for skipped tests
- 5.2.3 (2021-05-28)
  - Demotes a superfluous warning to a debug message
- 5.2.2 (2021-05-28)
  - Fixes a possibility of duplicate error messages in observation mode
- 5.2.0 (2021-05-28)
  - Adds observation mode
  - Adds optional anonymized telemetry
- 5.1.6 (2021-05-26)
  - Improves documentation
  - Improves log output
  - Fixes a bug where blank/absent/unreadable file paths for Python code would cause an error when traced
  - Fixes a bug where a remote dependency graph could be found and selected, but not used
  - In pytest, tests not run due to cohorting are now deselected (changed from selected but skipped)
  - Improved error handling in the face of `pytest-xdist`
  - Fixes a bug where a pytest run that selected 0 tests would be interpreted as failed
  - Fixes a bug where attaching to unittest hooks then using pytest to run a `unittest.TestCase` test would error
  - Standardizes terminology to "dependency graph" over "tracing data"
- 5.1.5 (2021-05-18)
  - When debug mode is on, debug output is now sent to both stdout and file (changed from just file)
- 5.1.4 (2021-05-18)
  - Fixes a bug with `unittest` support that could yield a blank dependency
    graph
  - Fixes a bug with `unittest` support that could cause a dependency graph to
    be written even for failed tests
- 5.1.3 (2021-05-18)
  - Fixes an error condition if `pytest` isn't installed
- 5.1.2 (2021-05-17)
  - Fixes CircleCI sharded environments from not being inherited by YourBase correctly
- 5.1.1 (2021-05-17)
  - Adds first-party support for test parallelization
- 5.0.10 (2021-05-13)
  - Fixes a compatibility issue with Celery
  - Fixes a compatibility issue with "proxy objects" causing tests to error
  - Improves error messages related to Git availability
- 5.0.9 (2021-05-11)
  - Fixes an issue processing certain styles of [PEP 263](https://www.python.org/dev/peps/pep-0263/) tags (e.g. `# -*- coding: utf-8 -*-`)
  - Adds some friendlier error messages and/or fallbacks caused by Git issues
- 5.0.7 (2021-05-06)
  - Fixes a JSON decoding issue present in Python 3.5
  - Fixes a breaking bug when YourBase is enabled alongside tests that use [`moto`](https://github.com/spulec/moto) mocks

See the [release history on our PyPI page](https://pypi.org/project/yourbase/#history).
