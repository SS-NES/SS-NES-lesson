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

For more information about DevOps see the [guide at github](https://github.com/resources/articles/devops/pipeline).

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

# Containers

Nowadays software is often distributed or deployed using containers.
These containers contain every dependency an application needs and can run anywhere.
This is especially useful for applications that run as a service on a cloud provider such as Google or Amazon Web Services where it is not known beforehand where an application will run.
These containers are light weight operating system images in which the application is stored including everything it needs.
CI/CD is extremely useful for automatically building such container images, as explained below in the section explaining pipelines and workflows.
Running applications in containers tends to enforce decoupling from external dependencies and communicating to external services through well defined and stable interfaces.
Building and distributing containers is generally done using [docker](https://www.docker.com) but there are others such as [podman](https://podman.io/)
You can find more information about containers [here](https://book.the-turing-way.org/reproducible-research/renv/renv-containers.html).

Publishing your application as a docker image is advised if the application has a lot of dependencies or if the build process is very complicated.
If the application is simple with only few dependencies, then creating a docker image probably creates too much overhead.
Docker is not suitable for publishing a module or library.
Here is a tutorial on 
[how to build docker images](https://book.the-turing-way.org/reproducible-research/renv/renv-containers.html#building-images-and-dockerignore-files)
Docker is a commercial application that has a community edition that can be used free of charge.
Usually the communitiy edition provides more than enough functionality.
[Podman](https://podman.io/) is a free and open source alternative for Docker if you prefer.

The docker website has a [list of guides](https://docs.docker.com/guides/) on creating docker images for all kinds of purposes.

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

Github workflows and alternatives from other suppliers enable you to trigger certain jobs on certain events.
For instance, you can configure it to only update the documentation if the only changes pushed to the repository are in the documentation.
Alternatively you can trigger it to build a release package only when merging to the main branch.
Check the [Understanding GitHub Actions guide](https://docs.github.com/en/actions/about-github-actions/understanding-github-actions) for all the possibilities.

Github Pages[13] is a workflow that works out of the box by configuring it on the repository's website[14]

[13]: https://docs.github.com/en/pages/getting-started-with-github-pages
[14]: https://docs.github.com/en/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site

Workflows are defined in the `.github/workflows` directory in a git repository.

Github has a [quick start tutorial](https://docs.github.com/en/actions/writing-workflows/quickstart) to get you started with workflows.

The example below will update the repository's GitHub Pages site when a changes is pushed to the `gh-pages` branch. As you can see, it will only build on pushing to the `gh-pages` branch.

```yaml
on:
  push:
    branches:
      - gh-pages

jobs: 
  publish-gh-pages:
    name: "Publish GitHub pages"
    runs-on: ubuntu-latest
    steps:
      - name: Configure GitHub Pages
        uses: actions/configure-pages@v5
```

## Run automated tests

## Build containers

- Reproducable, all dependencies, packages included.

Github[11] and docker[12] have tutorials on building docker container images in githhub workflows.

[11] https://github.com/actions/starter-workflows/blob/main/ci/docker-image.yml
[12] https://docs.docker.com/guides/gha/

## And more

Github provides a [collection][7] of starter workflows that you can build on.

[7]: https://github.com/actions/starter-workflows/tree/main

## Demo: From zero to published package in 15 minutes

### Step 1: Create a Python project

First step is to create a Python project on your personal computer.
There are several tools to help you with this.
In this tutorial we'll be using [Poetry](https://python-poetry.org/docs/basic-usage/).

```sh
poetry new demo-tdcc-nes
cd demo-tdcc-nes
```

Next turn the project into a git repository:

```sh
git init --initial-branch=main
```

And add the project's contents to it:

```sh
git add .
git commit -m "Initial commit"
```

### Step 2: Create a github repository and push the project to it

1. Go to https://github.com and login.
2. Click on "New" to create a new project and give it the name `demo-tddc-nes`.
3. Click "Create repository" at the bottom right. No need to change anything else.

Then push the project with the following commands:

```sh
git remote add origin git@github.com:<yourusername>/demo-tddc-nes.git
git push -u origin main
```

Refresh the page in the browser and you will see the contents of your project.

### Step 3: Create a python module and a test

With a text editor create a file `hello.py` in the `demo_tdcc_nes/` subfolder in the repository and paste the contents below.

```python
def hello(thing: str) -> str:
    return f"Hello {thing}"
```

Next, to create a test, create a folder `tests` in the repository top level directory:

```sh
mkdir tests
```

So, the repository should look like this:

```text
.
├── demo_tdcc_nes
│   ├── hello.py
│   └── __init__.py
├── pyproject.toml
├── README.md
└── tests
    └── __init__.py
```

Now create a file `test_hello.py` in the `tests` folder and paste the following content:

```python
import pytest

import demo_tdcc_nes
import demo_tdcc_nes.hello

@pytest.mark.parametrize('thing, expected', [("TDCC-NES", "Hello TDCC-NES")])
def test_hello(thing: str, expected: str) -> None:
    result = demo_tdcc_nes.hello.hello(thing)
    assert result == expected
```

install pytest package:

```sh
pipx install pytest
```

Then run the tests as follows:

```sh
pytest tests/
```

And examine the result of a passing test:

```txt
$ pytest tests/
================================================== test session starts ===================================================
platform linux -- Python 3.11.9, pytest-8.3.3, pluggy-1.5.0
rootdir: /home/user/projects/TDCC/demo-tdcc-nes
configfile: pyproject.toml
collected 1 item                                                                                                         

tests/test_hello.py .                                                                                              [100%]

=================================================== 1 passed in 0.01s ====================================================
$
```

### Step4: Commit the changes to git and push them to github

Type `git status` to show the files that have been added or have had their contents changed since the last commit.

```text
$ git status
On branch main
Your branch is up to date with 'origin/main'.

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        demo_tdcc_nes/hello.py
        tests/test_hello.py

nothing added to commit but untracked files present (use "git add" to track)
```

Stage the changes and commit:

```sh
git add demo_tdcc_nes/hello.py tests/test_hello.py
git commit -m "Implemented hello with test"
```

Next push the changes to github:

```sh
git push
```

### Step 5: Add a github actions workflow

The next step is to add a workflow to trigger github into creating a package and make it available.

Create the `.github/workflows` sub folder in the repository:

```sh
mkdir -p .github/workflows
```

The repository now should look like this:

```text
.
├── demo_tdcc_nes
│   ├── hello.py
│   ├── __init__.py
│   └── __pycache__
│       ├── hello.cpython-311.pyc
│       └── __init__.cpython-311.pyc
├── .github
│   └── workflows
├── pyproject.toml
├── README.md
└── tests
    ├── __init__.py
    ├── __pycache__
    │   ├── __init__.cpython-311.pyc
    │   └── test_hello.cpython-311-pytest-8.3.3.pyc
    └── test_hello.py
```

In the `.github/workflows` folder create the file `build-demo-tdcc-nes.yml`.
The name of the file is not very important, it's helpful however to choose a name that identifies what it does.
It should have the extension `.yml` or `.yaml` so it can be identifies as a yaml file.

Add the content below to the `.github/workflows/build-demo-tdcc-nes.yml` file:

```yaml
name: Upload Python Package

on: [push]

permissions:
  contents: read

jobs:
  release-build:
    runs-on: ubuntu-latest

    steps:
      - uses: actions/checkout@v4

      - uses: actions/setup-python@v5
        with:
          python-version: "3.12"

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

    steps:
      - name: Retrieve release distributions
        uses: actions/download-artifact@v4
        with:
          name: release-dists
          path: dist/
```

Stage the change, commit and push:

```sh
git add .github
git commit -m "Add packaging workflow"
git push
```

Click on the "Actions" tab in the github web page to see the workflow.
Then click on the workflow (it has the title of the `git commit` message).
A small graph is shown and at the bottom "release-dists" link is provided.
Click on that to download the package.

That's it! Package published!

### Step 6: Publishing the package to PyPi

You can publish the package to PyPi if you have an account at https://pypi.org/.
Follow the steps in the [Python Packaging User Guid](https://packaging.python.org/en/latest/tutorials/packaging-projects/) to make the package available through PyPi.

### Step 7: Additional workflow jobs

If you only want to trigger a certain workflow when there is a change in, for example, the `docs` directory, you can add the following in a separate wokflow file in the `.github/workflows` directory:

```yaml
on:
  push:
    paths:
      - 'docs/**'

jobs: 
  publish-gh-pages:
    name: "Publish GitHub pages"
    runs-on: ubuntu-latest
    steps:
      - name: Configure GitHub Pages
        uses: actions/configure-pages@v5
```

## Considerations

CI/CD pipelines are not very suitable if your tests require a lot of static data.
Running large integration tests inside a CI/CD pipeline is thus not recommended as there is generally limited space and time in CI/CD pipelines.
Writing small and fast unit tests that run automatically inside CI/CD pipelines rather than large integration tests is recommended.
It is therefore helpful to practice software engineering best practices such as decoupling, since that will lead to more easily testable code.
Larger integration tests can still be done in CI/CD as long as they don't require more than a few hundred megabytes of space and can complete within say 30 minutes.
Check the resource limits your CI/CD infrastructure provider (e.g. github or gitlab) imposes on CI/CD pipelines.
If you expect your tests to require more time and space than the CI/CD platform of you choice allows, consider alternative approaches such as [blue/green deployments](https://en.wikipedia.org/wiki/Blue%E2%80%93green_deployment).
Another alternative is to host your own pipeline runners that can be associated with your project on github[9] or gitlab[10].

[9]: https://docs.github.com/en/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners
[10]: https://gitlab.com/gitlab-org/gitlab-foss/-/blob/v17.5.0/doc/tutorials/create_register_first_runner/index.md
