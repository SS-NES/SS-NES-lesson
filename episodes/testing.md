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


# 1. Create the testing setup.


## use the SAD minimal template to get a correct setup

## Add some basic tests



# 2. Improve testing

## Add code coverage

What is code coverage? Code coverage is the percentage of the research / production code you have written that is covered by unittests. If you have a very high percentage then when you make a change in the code, and it breaks the chances of it being caught before showing it to users is very high. If you have a low percentage the chances of finding these bugs are low, or you have to do a lot of manual testing.  When working with python and pytest there are packages to easily get the test coverage of your application. The one used most is [pytest-cov](https://pytest-cov.readthedocs.io/en/latest/config.html) .

## Add parameterized tests

When writing tests it sometimes happens that you want a lot of tests for the same function. You could write a lot of test functions with the same setup and when calling the function under test some different parameters. A cleaner way where you have to maintain less code afterwards to do this is by using paramterized tests. With this you add the different parameters as inputs to you test function. An example of this looks like this:

```python
@pytest.mark.parametrize(
    ("onset", "phenomenon", "expected"),
    [
        (
            "2024-12-09T11:31:14Z",
            "snow-ice",
            "Monday 9 December: chance of snow/road icing",
        ),
        (
            "2025-01-04T00:00:00Z",
            "low-temperature",
            "Saturday 4 January: chance of cold",
        ),
    ],
    ids=["special_case", "normal_case"],
)
def test_get_english_headline(onset: str, phenomenon: str, expected: str) -> None:
    """test generation of english headline"""
    assert _get_english_headline({"onset": onset, "phenomenon": phenomenon}) == expected
```

As you can see even the expected result is now an input of the test. We can use the ids parameter to give a test a name. With this name you can also run the test for only one of the ids.


# 3. Testing a unit of software without having to instantiate the all the code

Sometimes it happens that you want to test function but in it a lot of complex objects are used that also need other objects. One way to deal with this is to add those complex objects as input to the function. You can that use this mock to prevent you having to create all those objects yourself.
In the code bellow we see the complex class being mocked and then given an implementation for when the method is called. This way we don't need to create input_one and input_two with all of there possible inputs.

```python
from unittest.mock import MagicMock

class Complex:
    
    def __init__(self, input_one, input_two):
        self.input_one = input_one
        self.input_two = input_two
    
    def execute(self):
        "do complex things"
        pass
    
def function_under_test(my_complex_object_with_multiple_inputs):
    return my_complex_object_with_multiple_inputs.execute()

def test_function_under_test():
    inputs = MagicMock()
    inputs.execute = MagicMock(return_value=3)
    result = function_under_test(inputs)
    expected = 3
    assert result == expected
    assert inputs.execute.call_count == 1
```

# 4. Working with external systems during a test



# 5 Performance testing of functions


# 6. Smoke testing to see if your application is still doing its basic functionality


# 7. Runtime testing

