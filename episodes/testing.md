---
title: "Intermediate software testing"
teaching: 90
exercises: 15
---

:::::: questions
 - How can I make changes to my research code while being sure existing functionality still works?
 - How can I execute the same test with multiple parameters?
 - What is code coverage and how can it help me verify the functionality of my code?
 - How do I create independent testing for my code without having to instantiate all the software?
 - How can I prevent dealing with external system during my tests?
 - How can I check if a given change improves the performance of my code?
 - How do I make sure that the application I have deployed for another party still works?
 - How can I make sure my programs stops when impossible cases are found?
::::::

:::::: objectives
 - Use pytest to write tests.
 - Use parameterized tests.
 - Use code coverage to have an idea of the confidence the system still works when changing the code.
 - Use mocks to mock out complex paths of code.
 - Use stubs to stub out complex paths of code.
 - Use performance testing tool to see if the speed of the code confirms to our demands.
 - Use smoke tests to do a quick check if the application should still run.
 - Use runtime testing to prevent weird cases. (hint to simulation testing?)
::::::

# Introduction

In this episode we are going to take a look at a few different types of automated testing. We will also see how we can use code coverage the increase our confidence that everything still works when we make a change to the code. There is an assumed base of having worked through the material on [this website](https://coderefinery.github.io/testing/motivation/). We will also make use of the [python template](https://github.com/SS-NES/python-template) to get a standardized starting point.



