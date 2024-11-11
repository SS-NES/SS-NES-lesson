---
title: "Continuous Integration"
teaching: 90
exercises: 15
---

:::::: questions

-   What is CI/CD?
-   Why do we use CI/CD?
-   What does CI/CD have to do with version control?
-   What is a CI/CD pipeline?
-   What is docker and how does it relate to CI/CD?
    ::::::

:::::: objectives

-   Understand what CI/CD is and why you would use it for your projects.
-   The relationship between CI/CD and version control
-   How to build a simple CI/CD pipeline
    ::::::

GOAL: create awareness or provide a tutorial?

# Continuous Integration and Continuous Deployment / Delivery

## Introduction

Continuous integration is the practice of integrating all your code changes
into the main branch of a shared source code repository early and often,
automatically testing each change when you commit or merge them, and
automatically kicking off a build. -- gitlab.com

Not to be confused with DevOps: CICD is _not_ DevOps, but DevOps requires CICD.
DevOps is the concept where a team is responsible for the entire life cycle of
a software product or software component. From development to deployment to
operating and maintaining it in production. Continuous Integration and
Continuous Delivery and/or Deployment plays a large role in this. But DevOps is
not required for leveraging CI/CD.

<https://github.com/resources/articles/devops/ci-cd>

We should distinguis Continuous Integration, Continuous Delivery and Continuous Deployment.

### Continuous Integration

Continuous integration is the practice of integrating all your code changes
into the main branch of a shared source code repository early and often,
automatically testing each change when you commit or merge them, and
automatically kicking off a build. With continuous integration, errors and
security issues can be identified and fixed more easily, and much earlier in
the development process. -- gitlab.com

### Continous Delivery

Continuous delivery is a software development practice that works in
conjunction with CI to automate the infrastructure provisioning and application
release process. -- gitlab.com

This can be understood as creating a Docker container, creating a PyPi package
for Python, a jar file for Java or equivalents for programming languages like R
or C/C++ and Fortran. This will be done in an automated way every time a change
is pushed to the git repository on github, or gitlab or some other platform.

### Continous Deployment

Continuous deployment enables organizations to deploy their applications
automatically, eliminating the need for human intervention. -- gitlab.com

When talking about deployment, we mean that the software is running on a server
and the services it provides are available for consumption by other sofftware
components. For research software that is the focus of this course, that is
rarely the case, so we ignore Continous Deployment and focus on Integration and Delivery.

## Why would we want Continuous Integration?

_Todo: needs more text_

- The earlier conflicts and bugs are discovered, the easier they are to fix.
- Deliver value to the user of the software quickly

# Version control

## Relationship between version control and CI/CD

_Todo: needs more text_

CICD relies on version control. Workflows are usually triggered by events, such
as merging to the main branch, happening on the verson control repository.

# Pipelines or workflows

_Todo: explain the concept of CI/CD pipelines / workflows_

## Pipeline stages

- verification, testing
- build
- deployment (Is this relevant for scientists who typically do not operate
  continuous running processes)
- Perhaps publishing packages to PyPi or similar

## Simple github workflow

<https://docs.github.com/en/actions/about-github-actions/understanding-github-actions>

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

-   Reproducable, all dependencies, packages included.

<https://github.com/actions/starter-workflows/blob/main/ci/docker-image.yml>

## Publish built package to PyPi

<https://docs.github.com/en/actions/use-cases-and-examples/building-and-testing/building-and-testing-python#publishing-to-pypi>
