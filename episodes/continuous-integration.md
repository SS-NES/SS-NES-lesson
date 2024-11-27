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

- Be able to explain the basic concepts of Continuous Integration and Continuous Delivery.
- Be able to explain (identify three reasons) why Continuous Integration and Continuous Delivery should be used.
- Be able to identify freely available tools and services to implement these concepts in a research context.
- Be able to explain the relationship between CI/CD and version control
- Be able to build a simple CI/CD pipeline or workflow
::::::

The main goal is to create awareness of the concept of Continuous Integration and Continuous Delivery and some of the tools to support it.

# Continuous Integration and Continuous Deployment / Delivery

## Introduction

The [Turing way][1] explains the concept very well.

Continuous Integration should not be confused with [DevOps][2]: CICD is _not_ DevOps, but DevOps effectively requires CICD.
DevOps is the concept where a team is responsible for the entire life cycle of a software product or software component.
From development to deployment to operating and maintaining it in production.
Continuous Integration and Continuous Delivery and/or Deployment plays a large role in this.
But DevOps is not required for leveraging CI/CD.

[1]: https://book.the-turing-way.org/reproducible-research/ci/ci-options "What is continuous integration?"
[2]: https://github.com/resources/articles/devops/ci-cd

We should distinguish Continuous Integration, Continuous Delivery and Continuous Deployment.

### Continuous Integration

> Continuous integration is the practice of integrating all your code changes
> into the main branch of a shared source code repository early and often,
> automatically testing each change when you commit or merge them, and
> automatically kicking off a build. With continuous integration, errors and
> security issues can be identified and fixed more easily, and much earlier in
> the development process. -- [gitlab.com][3]

[3]: https://about.gitlab.com/topics/ci-cd/#what-is-continuous-integration-ci "What is continuous integration?"

### Continous Delivery

> Continuous delivery is a software development practice that works in
> conjunction with CI to automate the infrastructure provisioning and
> application release process. -- [gitlab.com][4]

[4]: https://about.gitlab.com/topics/ci-cd/#what-is-continuous-delivery-cd "What is continuous delivery?"

This can be understood as creating a Docker container, creating a PyPi package for Python, a jar file for Java or equivalents for programming languages like R or C/C++ and Fortran.
This will be done in an automated way every time a change is pushed to the git repository on github, or gitlab or some other platform.

### Continous Deployment

> Continuous deployment enables organizations to deploy their applications
> automatically, eliminating the need for human intervention. -- [gitlab.com][5]

[5]: https://about.gitlab.com/topics/ci-cd/#what-is-continuous-deployment "What is continuous deployment?"

When talking about deployment, we mean that the software is running on a server and the services it provides are available for consumption by other software components.
For research software that is the focus of this course, that is rarely the case, so we ignore Continuous Deployment and focus on Integration and Delivery.

## Why is Continuous Integration and Continuous Delivery recommended?

CI/CD should be used when work is done in a collaborative project where changes created by different contributors need to be merged and tested.
The earlier in the process this is done, the easier any bugs or merge conflicts are to solve.

However, even in projects with a single developer utilizing CI/CD tools can be very benificial.
It will enable users of the software to have early access to it and bugs are discovered sooner.
It also enables the developer to run unit testing in an automated way to discover bugs early in the process.

- The earlier conflicts and bugs are discovered, the easier they are to fix.
- Deliver value to the user of the software quickly

# Version control

## Relationship between version control and CI/CD

CICD relies on version control.
Workflows are usually triggered by events, such as merging to the main branch happening on the verson control repository.

# Pipelines or workflows

> A CI/CD pipeline is an automated process utilized by software development teams to streamline the creation, testing and deployment of applications. -- [gitlab.com][6]

[6]: https://about.gitlab.com/topics/ci-cd/#what-are-ci-cd-pipelines "What are CI/CD pipelines"

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

## Github workflow publishing a package to PyPi

(From <https://docs.github.com/en/actions/use-cases-and-examples/building-and-testing/building-and-testing-python#publishing-to-pypi>)

```yaml
# This workflow uses actions that are not certified by GitHub.
# They are provided by a third-party and are governed by
# separate terms of service, privacy policy, and support
# documentation.

# GitHub recommends pinning actions to a commit SHA.
# To get a newer version, you will need to update the SHA.
# You can also reference a tag or branch, but the action may change without warning.

name: Upload Python Package

on:
  release:
    types: [published]

permissions:
  contents: read

jobs:
  release-build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-python@v5
        with:
          python-version: "3.x"

      - name: Build release distributions
        run: |
          # NOTE: put your own distribution build steps here.
          python -m pip install build
          python -m build

      - name: Upload distributions
        uses: actions/upload-artifact@v4
        with:
          name: release-dists
          path: dist/

  pypi-publish:
    runs-on: ubuntu-latest

    needs:
      - release-build

    permissions:
      # IMPORTANT: this permission is mandatory for trusted publishing
      id-token: write

    # Dedicated environments with protections for publishing are strongly recommended.
    environment:
      name: pypi
      # OPTIONAL: uncomment and update to include your PyPI project URL in the deployment status:
      # url: https://pypi.org/p/YOURPROJECT

    steps:
      - name: Retrieve release distributions
        uses: actions/download-artifact@v4
        with:
          name: release-dists
          path: dist/

      - name: Publish release distributions to PyPI
        uses: pypa/gh-action-pypi-publish@6f7e8d9c0b1a2c3d4e5f6a7b8c9d0e1f2a3b4c5d
```

## Run automated tests

## Build containers

- Reproducable, all dependencies, packages included.

<https://github.com/actions/starter-workflows/blob/main/ci/docker-image.yml>

## And more

Github provides a [collection][7] of starter workflows that you can build on.

[7]: https://github.com/actions/starter-workflows/tree/main

