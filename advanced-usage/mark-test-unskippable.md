---
layout: default
title: Mark a test as unskippable
nav_order: 1
parent: Advanced usage
permalink: /mark-test-unskippable
---

# Mark a test as unskippable
{: .no_toc }
If you have a test with external dependencies YourBase can't track, you can tell
YourBase's acceleration to never skip it using a decorator. The syntax differs slightly
based on which testing framework you're using.
- TOC
{:toc}

## pytest

```python
import pytest

@pytest.mark.do_not_accelerate
def test_function():
   ...
```

## unittest

```python
import yourbase.plugins.unittest as yourbase

@yourbase.do_not_accelerate
class TestClass(unittest.TestCase):
   def test_function():
      ...
```

## Testify

```python
import yourbase.plugins.testify as yourbase

@yourbase.do_not_accelerate
class TestClass(testify.TestCase):
    def test_function():
        ...
```
