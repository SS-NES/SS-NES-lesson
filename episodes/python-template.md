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

::::::::::::::::::::::::::::::::::::: challenge 

## Challenge 1: Can you do it?

What is the output of this command?

```r
paste("This", "new", "lesson", "looks", "good")
```

:::::::::::::::::::::::: solution 

## Output
 
```output
[1] "This new lesson looks good"
```

:::::::::::::::::::::::::::::::::


## Challenge 2: how do you nest solutions within challenge blocks?

:::::::::::::::::::::::: solution 

You can add a line with at least three colons and a `solution` tag.

:::::::::::::::::::::::::::::::::
::::::::::::::::::::::::::::::::::::::::::::::::

## Figures

You can use standard markdown for static figures with the following syntax:

`![optional caption that appears below the figure](figure url){alt='alt text for
accessibility purposes'}`

![You belong in The Carpentries!](https://raw.githubusercontent.com/carpentries/logo/master/Badge_Carpentries.svg){alt='Blue Carpentries hex person logo with no text.'}

::::::::::::::::::::::::::::::::::::: callout

Callout sections can highlight information.

They are sometimes used to emphasise particularly important points
but are also used in some lessons to present "asides": 
content that is not central to the narrative of the lesson,
e.g. by providing the answer to a commonly-asked question.

::::::::::::::::::::::::::::::::::::: keypoints 

- Use a template to implement best practices for you from the start
- Create a new repository using `copier copy gh:nlesc/python-template destination`
- Re-use the information from your SMP with the additional
  `--answers-file smp_answers.yaml` argument
- Add extra features to your project using `copier update`

::::::::::::::::::::::::::::::::::::::::::::::::

[r-markdown]: https://rmarkdown.rstudio.com/
[NLeSC Python Template]: https://github.com/NLeSC/python-template
