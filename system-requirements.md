---
layout: default
title: System requirements
nav_order: 2
has_children: false
permalink: /system-requirements
---

# System requirements
YourBase Test Acceleration is supported on the below technical stacks.

## Platforms
- Linux x86_64
- Linux ARM
- macOS Intel
- (experimental) macOS M1

(Run a stack that needs support? [Let us know!](mailto:python@yourbase.io))

## Languages & testing frameworks
YourBase supports the following testing frameworks and Python versions:
- [pytest](https://docs.pytest.org/en/6.2.x/) (Python 2.7 and 3.5+)
- [unittest](https://docs.python.org/3/library/unittest.html) (Python 2.7 and 3.5+)
- [django.test](https://docs.djangoproject.com/en/3.2/topics/testing/) (Python 2.7 and 3.5+)
- [Testify](https://github.com/yelp/testify) (Python 3.5+)

_Note: YourBase implicitly supports frameworks that extend any of the above frameworks._

## Version control
The library can accelerate tests only for codebases that are version-controlled using [Git](https://git-scm.com/). 

---

## That's it
YourBase Test Acceleration works seamlessly with the CI system of your choice and is agnostic to where you host your application—be it cloud, on-premise, or offline.
