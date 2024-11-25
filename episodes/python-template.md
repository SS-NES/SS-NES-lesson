---
title: "Generating a Repository using a Template"
teaching: 10
exercises: 2
---

:::::::::::::::::::::::::::::::::::::: questions 

- How can you quickly set up a new Python repository that follows best practices?

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

For people new to software development, this means you can trust in the prior
work of many other experienced people, and only have to focus on those parts
that are particularly relevant to your project. For experienced developers it
means you don't have to manually copy over the boilerplate code from a previous
project. This means you don't have to replace all your old values manually and
won't have a chance to accidentally forget some of them, while also keeping you
easily up to date with the latest and greatest instead of remaining stuck at
a previous point in time.

In both cases, using a trusted template will save you time, worries and make
sure your new projects are never outdated from the start.


:::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::: instructor

Inline instructor notes can help inform instructors of timing challenges
associated with the lessons. They appear in the "Instructor View"

::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::::

Install [`copier`]:

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
filled in for the SMP.


## Challenge 2: Reuse machine readable SMP tool output

The SMP tool provides a machine readable `yaml` file with all relevant answers
for creating a new project using this template. First remove the previous
project to make sure everything stays clean:

```bash
rm -rf path/to/destination
```

:::::::::::::::::::::::: solution 

```bash
copier copy --answer-file smp_answers.yaml gh:nlesc/python-template path/to/destination
```

:::::::::::::::::::::::::::::::::

Note how you were asked a lot fewer questions this time! Part of this is simply
filling in the information you already entered in the SMP. For the other
questions you weren't asked, the SMP tool has already suggested which set of
optional features best suit your project.

Because of a limitation in how `copier` handles these answer files, you don't
to review these choices when first creating your project. But luckily there is
a way to review the choices and to add extra features if you want.

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

