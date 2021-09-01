---
layout: default
title: System requirements
nav_order: 2
has_children: false
permalink: /system-requirements
---

# System requirements
YourBase Test Acceleration is supported on the below technical stack.

## Platforms
- Linux
- MacOS: All except those with the M1 chip

## Languages & testing frameworks
- Python 2.7+ and Python 3.5+ that use the following testing frameworks:
  - [pytest](https://docs.pytest.org/en/6.2.x/)
  - [unittest](https://docs.python.org/3/library/unittest.html)

_Note: Any web frameworks, such as [Django](https://www.djangoproject.com/), that are built atop the above testing frameworks, are also supported._

## Version control
The library can accelerate tests only for codebases that are version-controlled using [Git](https://git-scm.com/). 

---

## That's it
YourBase Test Acceleration works seamlessly with the CI system of your choice and is agnostic to where you host your application—be it cloud, on-premise, or offline.
