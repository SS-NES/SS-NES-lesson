---
title: "Explain the Decision Tree"
teaching: 10
exercises: 1
---


:::::::::::::::::::::::::::::::::::::: questions 

- Why did we introduce a decision tree at the beginning of our questionnaire?

::::::::::::::::::::::::::::::::::::::::::::::::

After introducing the name of your project and its purpose, you will enter the part of the tool that allows you to identify the relevant questions in the Software Management Plan for your project. We have constructed a decision tree that will guide you towards the minimum requirements for your SMP.

Figure
![Decision Tree Layout](../img/Decision_Tree_graphic.svg)

The reasoning behind the structure of the decision tree is to allow you to jump out of the process and into filling out the SMP as soon as possible. As you might notice from the figure above, the more people are involved in a project, the more complex the SMP is going to be.
With the same reasoning in mind, the least amount of people need to interact with your software, the least amount of bureaucracy you need to perform on it. This results in a shorter and more compact SMP.

:::::::::::::::::::::::::::::::::::::: Question 1

- Is your software going to be publically accessible?

::::::::::::::::::::::::::::::::::::::::::::::::

The first question you'll encounter in the decision tree is whether your software is going to be public or not. This question does not send you out of the decision tree and into the SMP document yet. Whether you choose yes or not, you will be forwarded to the next decision tree question.

What this question determines, however, is whether you will need to worry about seeting up a citation file and a license. If you answer "Yes", then citation and licensing are a point of interest, along with some basic user documentation to allow others to install and make use of your software.

If you answer "No", then only the purpose of your software and a risk analysis question will be taken to the document. As mentioned before, selecting "No" here will not result in you exiting the decision tree.

:::::::::::::::::::::::::::::::::::::: Question 2

- Is your software going to be reused after its initial purpose?

::::::::::::::::::::::::::::::::::::::::::::::::

This question is the first that lets you jump out of the Decision Tree and into filling in the SMP, should you choose "No". This is the case if your software is designed and intended for one time use. The SMP you need for it is going to be rather simple, since you do not need to maintain or expand the software. In general, the amount of people that are going to interact with your software is going estimated to be rather small. Especially if your software is not going to be public.

Should you instead choose "Yes" in this question, then your SMP will contain questions on the documentation that you will provide, as well as the testing that you set up to ensure that the software works as intended. Finally, a question on your software quality (and coding conventions) will be added to the SMP.

While it should be clear why documentation on the use, deployment, and development of software are useful when the software is being reused (by yourself or others), it is important to mention that proper testing and coding conventions go a long way towards making your software easy to use and reuse.

Testing ensures that you have a way of checking that everything works as intended for your software. This counts not only for when you are immediately working on it, but also when you have to come back to it after a medium to long break from developement. It can sometimes be hard to remember what you did and why if you haven't worked on the software for longer periods of time. Having tests built into the software make it easier to check the correct functionality in any given circumstance.

Finally, writing clean code with useful comments added inside it make it easier to follow what you were doing and why. This counts for yourself, but also for others. Another aspect of writing code by following conventions, is that your software is easier to read and understand if the format you use is widespread in the community.

 Let's consider a software that is in fact not going to be public (no to the first question) and not going to be reused after its initial purpose (no to the second question).

Introduce Case A

Moving on from this simple case, we add complexity as the number of people involved or impacted by your software grows. If your software is going to be reused, then at least one person will have to work with it again: you yourself. Even if you are the only one who will work with this software in the future, it is still a good idea to have documentation help you pin down decisions you made and functions of the software. If other people will be using the software, documentation is even more relevant.


The next question in the decision tree asks you if multiple users will be working with your software. This can vary between a small group of people you are in contact with or a larger group which you might not be able to provide support on yourself. 

Introduce the three main questions of the decision tree.
Multi-User
Reuse
Community
Knowledge of the consequences of opening up the software to a wider use.
What is the difference between multi-user and community?
Knowledge of the consequences of reusing the software
What is essential for others to reuse software not developed by them?
When is documentation enough?
Remarkable cases:
N/N/N - One time use, simplest plan needed
N/N/Y - One time use, but may need to be made public for verification purposes? Journal request?
Y/Y/N - Closed community?
Based on the information that you gathered from the decision tree, you can now understand the scope of a project and its potential impact.
Decision tree is stored in the JSON file, not the DOCX or the Cookiecutter file.
Should the “trainer” ask the researcher for decision tree information as well when checking SMP, if SMP is generated with our tool?
