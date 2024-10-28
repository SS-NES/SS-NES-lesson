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
 - Use code coverage to have an idea of the confidence the system still works when changing the code.
 - Use parameterized tests.
 - Use mocks to mock out complex paths of code.
 - Use stubs to stub out complex paths of code.
 - Use runtime testing to prevent weird cases. (hint to simulation testing?)
 - Use smoke tests to do a quick check if the application should still run.
 - Use performance testing tool to see if the speed of the code confirms to our demands.
::::::

