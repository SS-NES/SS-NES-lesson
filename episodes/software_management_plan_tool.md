---
title: "Software Management Plan Tool Questions"
teaching: 15
exercises: 5
---

:::::::::::::::::::::::::::::::::::::: questions

- How do you use the Software Management Plan (SMP) Tool?
- How to choose the correct answers for the SMP Tool?

::::::::::::::::::::::::::::::::::::::::::::::::

::::::::::::::::::::::::::::::::::::: objectives

- Understand how to navigate the SMP tool based on project impact
- Understand how to answer the questions in the SMP tool based on the information given and the resources provided

::::::::::::::::::::::::::::::::::::::::::::::::

## What is the SMP tool we have developed?

The SMP Tool is an online service and will be provided to you either by your organization or a third party. It is a questionnaire enriched with helpful resources which will provide you with an SMP upon completion. At the end of the questionnaire, you will be able to download different versions of the SMP for your project.

## How to Answer the SMP Questions

The answers provided to the questionnaire compose the content of your SMP. The more detail you can provide, the better your SMP will be. Keep in mind, however, that this is a living document evolving with your project and software, so "I don't know yet" can be a perfectly valid answer! It is encouraged to re-visit your SMP when the boundary conditions or the scope of your project becomes clearer or changes over time.

In the tool, you will find three distinct types of questions, which we will discuss in this lecture. These question types are: 
- "General" questions: Here you will provide the name of your software, the name of the developers, and other general details about your software, 
- "Decision Tree" questions: These questions help you identify the relevant questions for your software by estimating the impact and number of people dependent on your software,
- "Content" questions: These questions go into the details of your software management. 

The SMP Tool questions themselves will have detailed explanations and examples to aid the process of filling in the answers. For technical topics you might not yet be familiar with, there are links to resources that can help learning more about them. Therefore, we will focus more on the bigger picture in this lecture and address important topics of discussion first. After this more theoretical part, you will have a chance to try using the Software Management Plan Tool yourself.

### General Questions

In the section for "General" questions, you will be asked to fill in the details of your project, such as the name of your software, the participating members, the owner of the Intellectual Property, and the Organization where you will be developing your software, among other questions. This is generally the only section that you can fill in at any stage of the project and the one that might see the least amount of changes in the future, save for adding a new team member or organization.

Please make sure that the information given here is accurate and that especially the holder of the Intellectual Property of the software has been verified. More information on this can be found in the tool, but it is always a good idea to check with the legal department of your institution.

### Decision Tree
Part of the challenge in filling out a SMP is to understand and define which points in the SMP are relevant for your software. Depending on its scope and the impact you foresee it having, your software might need more attention in some areas of Software Management and less in others. The decision tree in the online questionnaire is meant to help you define what is relevant in the Plan by answering at most four simple questions. The figure below shows how the decision tree works.

Decision Tree
![Decision Tree Layout](../img/Decision_Tree_graphic.svg)

The reasoning behind the structure of the decision tree is to omit the questions that are not relevant for the scope of your software. As you might notice from the figure above, the more people are involved in a project, the more complex the SMP is going to be. On the flip-side, if less people interact with your software, the leaner a SMP can be. This results in a shorter and more compact SMP, tailored to your project.

#### Question 1: Is your software going to be publicly accessible?

The first question you'll encounter in the decision tree is whether your software is going to be public or not. This question does not send you out of the decision tree and into the content questions yet. Whether you choose yes or no, you will be forwarded to the next decision tree question.

What this question determines, however, is whether you will need to worry about setting up a citation file and a license. If you answer "Yes", then citation and licensing are a point of interest, along with some basic user documentation to allow others to install and make use of your software.

If you answer "No", then only the purpose of your software and a risk analysis question will be taken to the document. As mentioned before, selecting "No" here will not result in you exiting the decision tree.

#### Question 2: Is your software going to be reused after its initial purpose?

This question is the first that lets you jump out of the Decision Tree and into filling in the content questions, should you choose "No". This is the case if your software is designed and intended for one-time use. The SMP for this use-case is going to be rather simple, since you do not need to maintain or expand the software. In general, the amount of people that are going to interact with your software is going estimated to be rather small, especially if your software is not going to be public.

Should you instead choose "Yes" in this question, then your SMP will contain questions on the documentation that you will provide, as well as the testing that you set up to ensure that the software works as intended. Finally, a question on your software quality (and coding conventions) will be added to the SMP.

While it should be clear why documentation on the use, deployment, and development of software are useful when the software is being reused (by yourself or others), it is important to mention that proper testing and coding conventions go a long way towards making your software easy to use and reuse.

Testing ensures that you have a way of checking that everything works as intended for your software. This counts not only for when you are immediately working on it, but also when you have to come back to it after a medium to long break from development. It can sometimes be hard to remember what you did and why if you haven't worked on the software for longer periods of time. Having tests built into the software make it easier to check the correct functionality in any given circumstance.

Finally, writing clean code with useful comments added inside it make it easier to follow what you were doing and why. This counts for yourself, but also for others. Another aspect of writing code by following conventions, is that your software is easier to read and understand if the format you use is widespread in the community.

#### Question 3: Is your software going to have multiple users working on it?

The difference between the answer to this question and the answer to the previous one, is that for the software to be reused, you do not require people to work on the software itself. For this question, we intend to ask if you expect multiple other people to active modify or contribute to the software.

Should you answer "No" here, then the SMP will not contain more questions than the ones added with the previous question. Please take into account that if development is done by other people and not just you, the answer to this question is "Yes", even if you are the main user of the software.

If you answered "Yes", then the complexity of your software increases just by the fact that more and more people are able to change and add to it. This means that the management needed to ensure that your software is working and maintained properly increases with the amount of people involved. More questions will be added to the SMP if this is the case.

Having multiple users involved in your software means that topics such as the packaging of your software, as well as the maintenance of it become relevant. These questions will be added to the SMP document that you have to fill out on top of what was already selected for multiple users.

#### Question 4: Is your software going to grow a community around it?

This is the last question in the decision tree. Answering "Yes" here will mean that the entirety of the SMP will be selected for you to fill out. The difference between a community and multiple users working on your software is intended to be the difference between a group of people that you can be in contact with personally, and a group of people with whom you might not have personal contact.

If you answer "No" here, you will simply exit the Decision Tree with all the questions selected in Question 3 of the decision tree. Please keep in mind that multiple users can evolve into a community over time, so some of the topics skipped in Question 3 might become relevant later on. Should this be the case, please make sure to revise your SMP to fit the new reality of your software.

Should you answer "Yes" here, then you will add questions on the sustainability of your software, as well as the support you plan to provide to your users. Sustainability is important if a community grows around your software, because you might not be able to respond to changes happening to resources your software needs. Having a sustainability plan and contingencies in place early on will help you face sudden changes later. You don't need to have fool-proof plan yet, but already considering the issue will help you deal with it, should the occasion arise.

Finally, setting up support in case you have a growing community will ensure that you can keep your software working for all kinds of users.

### Content Questions

TODO

## Exercises:

Based on the information that you gathered from the decision tree, you can now understand the scope of a project and its potential impact. To help you test out how the Decision Tree works in practice, we have two examples of software here, for which an SMP needs to be filled in. Please read the examples and think about which questions can be answered in the positive in the Decision Tree.

N.B.: If you have your own example software to do this exercise with, please feel free to use it.

### Challenge 1: Use the Decision Tree to estimate the impact of the software described below.


```r
The software in question are scripts run to extract data from an astronomical image. The scripts identify areas where light/signal is present in the image and extract the measured light spectrum of the pixels for which the signal-to-noise is above a value of 5. The scripts also provide the location of the brightest pixel per object and create easy to read ASCII files to plot the spectrum of the various light sources.

The author of the scripts has decided to store them on a GitLab instance present at their instiute. The GitLab repository is referenced in their paper, should someone want to verify the results obtained with the scripts. These scripts are based on known methods to extract data from an astronomical image. 
```

:::::::::::::::::::::::: solution 
 
```
Depending on if you see verification as a form of reuse or not, two answers are possible, as shown below. The script will not be further modified or expanded by others, so there are not multiple users involved. Question 3 should be the latest point where you answer no.

Either: 
1) Yes 2) Yes 3) No 4) -
Or:
1) Yes 2) No 3) - 4) -
```

:::::::::::::::::::::::::::::::::


### Challenge 2: And what does the Decision Tree look like for this other software?

```r
As a result of an internal project, a software has been developed to track and predict convective cells in the atmosphere (i.e. Thunderstorms). A team of software engineers and other experts is working on this software to expand and better its functionality. The project itself is still ongoing and the software has yet to be published in a repository. Plans for its publication will eventually be discussed at the end of the project.
```
:::::::::::::::::::::::: solution 

```
The project is still internal and will stay internal for a longer period of time, so the first question is a negative. Questions two and three are yes, because the scope of the project is to reuse the software and multiple people are involved in using and coding the software. Question 4 is no, as a community will most likely only build itself, if the software gets published.

1) No 2) Yes 3) Yes 4) No
```

:::::::::::::::::::::::::::::::::

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

- The SMP Tool uses a decision tree to determine the relevant content questions
  - Simple software projects require less information
- The SMP Tool creates three output files
  - A human-readable SMP
  - A machine-readable SMP (JSON dump of all answers) for custom processing
  - Machine-readable SMP information as input for the [NLeSC Python Template](https://github.com/NLeSC/python-template) (YAML format)
- TODO

::::::::::::::::::::::::::::::::::::::::::::::::
