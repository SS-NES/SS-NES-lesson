---
title: "Continuous Integration"
teaching: 90
exercises: 15
---

:::::: questions
 - What is CI/CD?
 - Why do we use CI/CD?
 - What does CI/CD have to do with version control?
 - What is a CI/CD pipeline?
 - What is docker and how does it relate to CI/CD?
::::::

:::::: objectives
 - Understand what CI/CD is and why you would use it for your projects.
 - The relationship between CI/CD and version control
 - How to build a simple CI/CD pipeline
::::::

GOAL: create awareness or provide a tutorial?

# Continuous Integration and Continuous Deployment

## Introduction

CICD is _not_ DevOps, but DevOps requires CICD.

https://github.com/resources/articles/devops/ci-cd

Continuous integration is the practice of integrating all your code changes into the main branch of a shared source code repository early and often, automatically testing each change when you commit or merge them, and automatically kicking off a build. -- gitlab.com

## Why?

- The earlier conflicts and bugs are discovered, the easier they are to fix.
- Deliver value to the user of the software quickly

# Version control

## Relationship between version control and CI/CD

CICD relies on version control. Workflows are usually triggered by events, such as merging to the main branch, happening on the verson control repository.

# Pipelines

## Pipeline stages

- verification, testing
- build
- deployment (Is this relevant for scientists who typically do not operate continuous running processes)
  - Perhaps publishing packages to PyPi or similar

## Simple github workflow

https://docs.github.com/en/actions/about-github-actions/understanding-github-actions

Workflows are defined in the `.github/workflows` directory in a git repository.

```yaml
name: Run unit tests

on: [push]

jobs:
    build:
    runs-on: ubuntu-latest
    strategy:
        matrix:
            python-version: ["3.12"]
    steps:
    - uses: actions/checkout@v4
    - name: Set up Python
    uses: actions/setup-python@v5
    with:
        python-version: '3.x'
    - name: Install dependencies
    run: |
        python -m pip install --upgrade pip
        pip install -r requirements.txt
    - name: Test with pytest
    run: |
        pip install pytest pytest-cov
        pytest tests.py --doctest-modules --junitxml=junit/test-results.xml --cov=com --cov-report=xml --cov-report=html
```

## Run automated tests

## Build containers

- Reproducable, all dependencies, packages included.

https://github.com/actions/starter-workflows/blob/main/ci/docker-image.yml

## Publish built package to PyPi

https://docs.github.com/en/actions/use-cases-and-examples/building-and-testing/building-and-testing-python#publishing-to-pypi
