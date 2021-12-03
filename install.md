---
layout: default
title: Installation
nav_order: 2
has_children: false
permalink: /install
---

# Install
{:.no_toc}

Table of contents
{: .text-delta }

1. TOC
{:toc}

---

## Prerequisites
Make sure that the YourBase Test Acceleration library [supports your technical stack and infrastructure](system-requirements.md).

## Installation

YourBase Test Acceleration can be installed with your standard Python package manager,
e.g. [pip](https://pip.pypa.io/en/stable/) or [poetry](https://python-poetry.org/docs/).

```sh
# pip
pip install yourbase
# poetry
poestry add yourbase
```

Alternatively, add `yourbase` to your `requirements.txt` or similar.


## Recommendations

### Use a virtual environment
{: .no_toc }

We recommend that you install YourBase Test Acceleration in a clean virtual environment.
[Learn to set up a Python virtual environment
here](https://docs.python.org/3/tutorial/venv.html).

---

## Uninstall
If for any reason, you want to completely remove YourBase Test Acceleration, simply uninstall the package:

Using [pip](https://pip.pypa.io/en/stable/): 

```sh
# pip
pip uninstall yourbase
# poetry
poetry remove yourbase
```



