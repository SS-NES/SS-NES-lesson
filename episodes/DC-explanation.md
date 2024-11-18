---
title: "Explain the Decision Tree"
teaching: 10
exercises: 1
---

## Why did we introduce a decision tree at the beginning of our questionnaire?

Part of the challenge in filling out a Software Management Plan (SMP) is to understand and define which points in the SMP are important, or even relevant, for your software. Depending on its scope and the impact you foresee it having, your software might need more attention in some areas of Software Management and less in others. We have decided to introduce a Decision Tree in our online questionnaire to help you define what is relevant in the Plan by answering at most four simple questions. And so, after introducing the name of your project and its purpose, you will enter the Decision Tree part of the tool. The figure below shows how the decision tree works:

Figure
![Decision Tree Layout](../img/Decision_Tree_graphic.svg)

The reasoning behind the structure of the decision tree is to allow you to jump out of the process and into filling out the SMP as soon as possible. As you might notice from the figure above, the more people are involved in a project, the more complex the SMP is going to be.
With the same reasoning in mind, the least amount of people need to interact with your software, the least amount of bureaucracy you need to perform on it. This results in a shorter and more compact SMP.

## Question 1: Is your software going to be publically accessible?


The first question you'll encounter in the decision tree is whether your software is going to be public or not. This question does not send you out of the decision tree and into the SMP document yet. Whether you choose yes or not, you will be forwarded to the next decision tree question.

What this question determines, however, is whether you will need to worry about seeting up a citation file and a license. If you answer "Yes", then citation and licensing are a point of interest, along with some basic user documentation to allow others to install and make use of your software.

If you answer "No", then only the purpose of your software and a risk analysis question will be taken to the document. As mentioned before, selecting "No" here will not result in you exiting the decision tree.

## Question 2: Is your software going to be reused after its initial purpose?

This question is the first that lets you jump out of the Decision Tree and into filling in the SMP, should you choose "No". This is the case if your software is designed and intended for one time use. The SMP you need for it is going to be rather simple, since you do not need to maintain or expand the software. In general, the amount of people that are going to interact with your software is going estimated to be rather small. Especially if your software is not going to be public.

Should you instead choose "Yes" in this question, then your SMP will contain questions on the documentation that you will provide, as well as the testing that you set up to ensure that the software works as intended. Finally, a question on your software quality (and coding conventions) will be added to the SMP.

While it should be clear why documentation on the use, deployment, and development of software are useful when the software is being reused (by yourself or others), it is important to mention that proper testing and coding conventions go a long way towards making your software easy to use and reuse.

Testing ensures that you have a way of checking that everything works as intended for your software. This counts not only for when you are immediately working on it, but also when you have to come back to it after a medium to long break from developement. It can sometimes be hard to remember what you did and why if you haven't worked on the software for longer periods of time. Having tests built into the software make it easier to check the correct functionality in any given circumstance.

Finally, writing clean code with useful comments added inside it make it easier to follow what you were doing and why. This counts for yourself, but also for others. Another aspect of writing code by following conventions, is that your software is easier to read and understand if the format you use is widespread in the community.


## Question 3: Is your software going to multiple users working on it?

The difference between the answer to this question and the answer to the previous one, is that for the software to be reused, you do not require people to work on the software itself. For this question, we intend to ask if you expect multiple other people to active modify or contribute to the software. 

Should you answer "No" here, then the SMP will not contain more questions than the ones added with the previous question. Please take into account that if development is done by other people and not just you, the answer to this question is "Yes", even if you are the main user of the software.

If you answered "Yes", then the complexity of your software increases just by the fact that more and more people are able to change and add to it. This means that the management needed to ensure that your software is working and manintained properly increases with the amount of people involved. More questions will be added to the SMP if this is the case.

Having multiple users involved in your software means that topics such as the packaging of your software, as well as the maintenance of it become relevant. These questions will be added to the SMP document that you have to fill out on top of what was already selected for multiple users.


## Question 4: Is your software going to grow a community around it?

This is the last question in the Decision Tree. Answering "Yes" here will mean that the entirety of the SMP will be selected for you to fill out. The difference between a community and multiple users working on your software is intended to be the difference between a group of people that you can be in contact with personally, and a group of people with whom you might not have personal contact.

If you answer "No" here, you will simply exit the Decision Tree with all the questions selected in question 3. Please keep in mind that multiple users can evolve into a community over time, so some of the topics skipped in Question 3 might become relevant later on. Should this be the case, please make sure to revise your SMP to fit the new reality of your software.

Should you answer "Yes" here, then you will add questions on the sustainability of your software, as well as the support you plan to provide to your users. Sustainability is important if a community grows around your software, because you might not be able to respond to changes happening to resources your software needs. Having a sustainability plan and contingencies in place early on will help you face sudden changes later. You don't need to have fool-proof plan yet, but already considering the issue will help you deal with it, should the occasion arise.

Finally, setting up support in case you have a growing community will ensure that you can keep your software working for all kinds of users.

## Exercises: 

Based on the information that you gathered from the decision tree, you can now understand the scope of a project and its potential impact.

## Challenge 1: Use the Decision Tree to estimate the impact of the software described below.


```r
Software Description...
```

:::::::::::::::::::::::: solution 
 
```
1) Yes 2) No 3) - 4) -
```

:::::::::::::::::::::::::::::::::


## Challenge 2: And what does the Decision Tree look like for this other software?

```r
Software Description...
```
:::::::::::::::::::::::: solution 

```
1) Yes 2) Yes 3) Yes 4) No
```

:::::::::::::::::::::::::::::::::


Add this last part to the pull request, not the .md file!!
Decision tree is stored in the JSON file, not the DOCX or the Cookiecutter file.
Should the “trainer” ask the researcher for decision tree information as well when checking SMP, if SMP is generated with our tool?
