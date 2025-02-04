---
title: "Introduction"
teaching: 10
exercises: 10
---

:::::::::::::::::::::::::::::::::::::: questions

- What is a Software Management Plan (SMP)?
- Why is an SMP important?
- How is an SMP useful?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understand the role of a Software Management Plan (SMP).
- Understand that the stage and scope of your software can determine that some parts of the SMP are not relevant (yet).
- Understand that no matter the scope of your software, an SMP is always relevant.

::::::::::::::::::::::::::::::::::::::::::::::::

## Introduction

A Software Management Plan (SMP) is a formal document explaining how software is written and managed both during and after a research project. It is a living document and will evolve with the boundary conditions of your project and software. While it is encouraged to write an SMP _before_ starting to develop code, it is never too late to create one for existing projects.

### Importance

SMPs provide value both inside and outside your organization. It encourages you to think about the roles and responsibilities within the project and gives guidance for new team members. Writing an SMP will guide you through the best practices that you can apply to your software based on the size and scope of your project. Following the best practices outlined in an SMP will make it easier for others to use or cite your software. For all of the above reasons some research funders start to require an SMP to be included in proposals.

## General Workflow

The SMP Tool is an online service and will be provided to you either by your organization or a third party. It is a questionnaire which will provide you with an SMP upon completion.

It starts out with a few questions relevant for projects, like the general goal of the project. Then you will be presented with a few questions that define the scope of your project. These are a "decision tree" that can switch on or off many of the following "content questions" which tailor the content of the SMP to the scope of your project.

After you complete the questionnaire you can download different versions of the SMP for your project.

## Output Files

You can download your SMP in three different variants. The first one is a human-readable Word document. For many projects this is all that is needed.

The second variant is a machine-readable copy of _all_ the provided answers in JSON format. This can be used as a backup of the provided data and for custom processing in your own workflows.

The third and last variant contains machine-readable SMP information in YAML format that can be used as input for the [NLeSC Python Template](https://github.com/NLeSC/python-template) to start a new software project.

## Exercises:

The SMP Tool provides you with several output files for different purposes. What benefit can they give you?


### Challenge 1: How could you use the machine-readable JSON output?


```r
The machine-readable JSON output contains all the supplied answers. There is no ready-made tooling yet to consume it, but you can create your own. For which purposes could this be useful?
```

:::::::::::::::::::::::: solution

```
1) The machine-readable JSON output is a backup of all your supplied answers. You can use it when you re-visit the SMP Tool in the future to incorporate changes in boundary conditions or project scope.
2) Having a machine-readable SMP enables you to consume the data in other tools. This could be a compliance checker that tests your projects for applied best practices, a tool that charts license usage across projects, or a script that maps authors to projects.
```

:::::::::::::::::::::::::::::::::

### Challenge 2: How can you use the machine-readable YAML output?


```r
The YAML output can be consumed by the [NLeSC Python Template](https://github.com/NLeSC/python-template) for starting a Python project. What is the workflow here? Read up about the template and understand how it can help your project.
```

:::::::::::::::::::::::: solution
 
```
TODO
```

:::::::::::::::::::::::::::::::::

### Challenge 3: Which of the output files would be useful for your own project?


```r
Imagine how you could use the different output files for your own project.
```

:::::::::::::::::::::::: solution
 
```
Free discussion
```

:::::::::::::::::::::::::::::::::


::::::::::::::::::::::::::::::::::::: keypoints

- A SMP is valuable in any stage of your project
  - It outlines how the software supports the vision of your project
  - It encourages you to follow best practices based on the scope of your project
- The SMP Tool uses a decision tree to determine the relevant content questions
  - Simple software projects require less information
- The SMP Tool creates three output files
  - A human-readable SMP
  - A machine-readable SMP (JSON dump of all answers) for custom processing
  - Machine-readable SMP information as input for the [NLeSC Python Template](https://github.com/NLeSC/python-template) (YAML format)

::::::::::::::::::::::::::::::::::::::::::::::::
