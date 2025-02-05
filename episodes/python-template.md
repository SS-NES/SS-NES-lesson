---
title: "Generating a Repository using a Template"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions

- What is the fastest way to set up a new Python repository that suits your needs?
- How do you make sure this repository follows best practices?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Explain why you should use a template to start a new repository
- Demonstrate how to create a repository using the [NLeSC Python Template]
- Demonstrate how to use the upgrade feature of [`copier`] to extend your
  repository with extra features

::::::::::::::::::::::::::::::::::::::::::::::::

## Why use a template?

No matter how (in)experienced a programmer you are, using a template when
starting a new project is always a good idea. Templates let you easily make
use of the latest and greatest in best practices, without having to reinvent
the wheel for every project.

As someone who is new to programming, employing a template can help you to setup
your first projects and help you adhere to coding standards such that your
software can be understood by others. In general employing templates saves time
and helps to prevent confusion when copy pasting from old repositories. E.g.
parameters and specific configurations are easily overlooked and not being
edited.

In both cases, using a trusted template will save you time, worries and make
sure your new projects are never outdated from the start.


:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

Using `pipx` to install copier is recommended, so it doesn't pollute the
global environment of the user, and so they don't have to install it in their
(not-yet-existant) project space. It's only recommended to let participants
deviate from this advice and directly `pip install copier` if they (confidently)
know what they're doing.

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

A popular tool for using and applying templates is the Python tool [`copier`].
Using `copier`, you can create a project based on a template made by yourself
or someone else. Templates can be configured to ask you some questions for
details that `copier` will then fill in throughout the files to personalize it
to suit your needs.

The recommended way to install `copier` as a local tool is using `pipx`:

```bash
python3 -m pip install --user pipx
python3 -m pipx --ensurepath
pipx install copier
```

Now you can use `copier` as a standalone tool to create new projects.

::::::::::::::::::::::::::::::::::::: challenge

## Challenge 1: Use the NLeSC Python Template

Create a new project based on the Python template by the Netherlands eScience Center:

:::::::::::::::::::::::: solution

```bash
copier copy gh:nlesc/python-template path/to/destination
```

:::::::::::::::::::::::::::::::::


::::::::::::::::::::::::: callout

Copier can create a project from a local folder and from a remote git
repository URL such as [https://github.com/nlesc/python-template.git].
The following shortcut URLs are also supported:

- GitHub: `gh:namespace/project`
- GitLab: `gl:namespace/project`

:::::::::::::::::::::::::::::::::

Notice how you are asked to answer a lot of basic information that you already
filled in for the SMP in the previous episode.


## Challenge 2: Reuse machine readable SMP tool output

The SMP tool provides a machine readable `yaml` file with all relevant answers
for creating a new project using this template. First remove the previous
project to make sure everything stays clean:

```bash
rm -rf path/to/destination
```

:::::::::::::::::::::::: solution

```bash
copier copy --answers-file smp_answers.yaml gh:nlesc/python-template path/to/destination
```

:::::::::::::::::::::::::::::::::

Note how you were asked a lot fewer questions this time! Part of this is simply
filling in the information you already entered in the SMP. For the other
questions you weren't asked, the SMP tool has already suggested which set of
optional features best suit your project.

Due to the limitation how `copier` handles the answer files, you also cannot
review choices you made in the SMP. In the next section, you will see how you
can add or change features of your code repository.

## Challenge 3: Add more features to your project

Use `copier`'s `update` functionality to add extra features to your project.

:::::::::::::::::::::::: solution

```bash
cd path/to/destination  # copier update must run from within your project
copier update
```

:::::::::::::::::::::::::::::::::

That's all folks!

::::::::::::::::::::::::::::::::::::::::::::::::



::::::::::::::::::::::::::::::::::::: keypoints

- Use a template to implement best practices for you from the start
- Create a new repository using `copier copy gh:nlesc/python-template path/to/destination`
- Re-use the information from your SMP with the additional
  `--answers-file smp_answers.yaml` argument
- Add extra features to your project using `copier update`

::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
[NLeSC Python Template]: https://github.com/NLeSC/python-template
[https://github.com/nlesc/python-template.git]: https://github.com/NLeSC/python-template.git

