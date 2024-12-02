---
title: "Intermediate software testing"
teaching: 60
exercises: 0
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


# 1. Improve testing

## Add code coverage

What is code coverage? Code coverage is the percentage of the research / production code you have written that is covered by [unittests](https://book.the-turing-way.org/reproducible-research/testing/testing-unittest). If you have a very high percentage then when you make a change in the code, and it breaks the chances of it being caught before showing it to users is very high. If you have a low percentage the chances of finding these bugs are low, or you have to do a lot of manual testing.  When working with python and pytest there are packages to easily get the test coverage of your application. The one used most is [pytest-cov](https://pytest-cov.readthedocs.io/en/latest/config.html) .

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
For more information on parameterized tests you can read [this how-to guide](https://docs.pytest.org/en/stable/how-to/parametrize.html#pytest-mark-parametrize).

# 2. Testing a unit of software without having to instantiate all the code

Sometimes it happens that you want to test a function but in that function a lot of complex objects are used (and those objects in turn need other objects...). One way to deal with this is to add those complex objects as input to the function. You can that use this mock to prevent you having to create all those objects yourself.
In the code bellow we see the complex class being mocked and then given an implementation for when the method is called. This way we don't need to create `input_one `and `input_two `with all of their possible inputs. This type of test double tests state and behaviour.

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
For more information on mocking you can read [this quick guide](https://docs.python.org/3/library/unittest.mock.html#quick-guide).
Another way to not have to create the whole object graph is to use a fake. A fake a class that looks like the class it fakes (so inheritance is possible here) and has the methods that we want to test override. This type of test double tests state.

```python
class Complex:

    def __init__(self, input_one, input_two):
        self.input_one = input_one
        self.input_two = input_two

    def execute(self):
        "do complex things"
        pass


def function_under_test(my_complex_object_with_multiple_inputs):
    return my_complex_object_with_multiple_inputs.execute()

class ComplexFake(Complex):
    def __init__(self):
        pass

    def execute(self):
        return 3

def test_function_under_test():
    inputs = ComplexFake()
    result = function_under_test(inputs)
    expected = 3
    assert result == expected
```

# 3. Working with external systems during a test

When writing code you do not always have the data on your machine. Sometimes you need to download data over http. For this a lot of the time people use the requests library (when you have async code aiohttp is a nice alternative). For your unit test however you don't want to be dependent on the network, because this is unreliable and can have your tests sometimes fail for no reason. One way is to split the http call inside another method and use a fake response when testing that method. The following code calls the german weather opendata platform to get thunderstorm data. The page gets a lot of updates in the data but the format stay's the same. The actual api calls can then be tested inside an integration test and also look at the error handling. More information about integration testing can be found at [the turing way](https://book.the-turing-way.org/reproducible-research/testing/testing-integrationtest).

```python
import requests
from bs4 import BeautifulSoup
from unittest.mock import patch

def get_konrad3d_data(url):
    response = requests.get(url)
    return response.text

def extract_latest_file(overview_page):
    soup = BeautifulSoup(overview_page, features="html.parser")
    urls = soup.find_all('a')
    latest_file = urls[-1].get('href')
    return latest_file

def get_latest_file_konrad3d():
    url = "https://opendata.dwd.de/weather/radar/konrad3d/"
    overview_page = get_konrad3d_data(url)
    latest_file = extract_latest_file(overview_page)
    return latest_file

data = '<html><head><title>Index of /weather/radar/konrad3d/</title></head><body><h1>Index of /weather/radar/konrad3d/</h1><hr><pre><a href="../">../</a><a href="KONRAD3D_20241116T093000.xml">KONRAD3D_20241116T093000.xml</a>                       16-Nov-2024 09:34                3895<a href="KONRAD3D_20241118T092500.xml">KONRAD3D_20241118T092500.xml</a>                       18-Nov-2024 09:30                3938</pre><hr></body></html>'

def test_download_latest_data_konrad3d():
    with patch("faketest.get_konrad3d_data", return_value=data):
        result = get_latest_file_konrad3d()
    expected = "KONRAD3D_20241118T092500.xml"
    assert result == expected
```

Another way to not do these API calls is by using the [requests_mock library](https://pypi.org/project/requests-mock/) to mock requests API calls. This makes you dependent on another library and still does not show you if things work in reality. It's being used by a lot of people, but personally I prefer fewer dependencies and write integration tests for the integration with external systems.  When you mock this it can give you a false sense of security like happened with the Crowdstrike outage in their testing. If you want to use this an example can be found bellow.

```python
import requests
import requests_mock

def get_konrad3d_data(url):
    response = requests.get(url)
    return response.text

def test_download_latest_data_konrad3d():
    data = '<html><head><title>Index of /weather/radar/konrad3d/</title></head><body><h1>Index of /weather/radar/konrad3d/</h1><hr><pre><a href="../">../</a><a href="KONRAD3D_20241116T093000.xml">KONRAD3D_20241116T093000.xml</a>                       16-Nov-2024 09:34                3895<a href="KONRAD3D_20241118T092500.xml">KONRAD3D_20241118T092500.xml</a>                       18-Nov-2024 09:30                3938</pre><hr></body></html>'
    url = 'https://opendata.dwd.de/weather/radar/konrad3d/'
    with requests_mock.Mocker() as m:
        m.get(url, text=data)
        result = get_konrad3d_data(url)
    assert result == data
```

# 4 Performance testing of functions

There are moments that the performance of you function might matter a lot. You might not want a single function to ever execute slower than x seconds. To test this you could write tests for the specific functions that should stay fast. How this works is that you run a function x amount of times and the max duration of the function should not be higher than the x seconds. A useful library to help with these types of test in python is [pytest-benchmark](https://pytest-benchmark.readthedocs.io/en/stable/pedantic.html). This library can also be used to check if the performance between versions of the code is improved.

```python
import time
def function_to_test(duration=1):
    time.sleep(duration)
    return 123

def test_my_function(benchmark):
    allowed_speed = 1.000002
    result = benchmark.pedantic(function_to_test, iterations=5)
    assert benchmark.stats.stats.max < allowed_speed

    assert result == 123
```

This code can be run with the following command: `pytest -v -s the file_this_is_in.py::test_my_function`. It will run the code 5 times and none of the calls is allowed to be slower than the allowed_speed.

When you write API's you can also have performance requirements. For this another type of tool is used. One of the most used tools for this in python is locust. FOr more information about this tool look you can look at [their documentation](https://docs.locust.io/en/stable/what-is-locust.html).

# 5. Smoke testing to see if your application is still doing its basic functionality

There are moments that you want to start an application but the application has some prerequisites it needs to have before you can say that it's good and allowed to run. For this you can use a smoke tests. For example when you have an application that when a user calls it reads configurations files from a file system the check could be if the files exist at the correct location and the format is as expected. Maybe someone manually moved the files it this could break the whole system. So when the files are not there, there is smoke and thus if it's production we could get a fire. In the example bellow you could see how to test something like this in the same application. However, most of the time those checks would be in another script before you start this script (or if you use Kubernetes an init container).

```python
def config_file_is_found():
    #check on location if file exists
    pass

def main():
     #application logic
    pass

if __name__ == '__main__':
    if not config_file_is_found(): 
        raise FileNotFoundError("our config file is not found")
    main()
```

More information about smoke tests can be found on [the turing way](https://book.the-turing-way.org/reproducible-research/testing/testing-smoketest).

# 6. Runtime testing

When software is in production, and you introduce a new path inside the code you might want to run it for a while without actually implementing the behaviour inside that code path. And example for this is that when we implemented an extra validation for our public dataplatform we first added the validation where we allowed everything like before. But we executed the new logic and logged all unexpected things that happened. This gave us a lot of information about what would happen when we would turn the feature on for real. One important thing we found out that inside our network some http requests would only reach their destination after 10+ seconds. The application would already have given the users an error and that's not what we wanted. Because of this information we could add a solution that when we eventually brought our check live no users got an error.

An example of a check like this can be found bellow.

```python
def my_new_validation_logic_to_external_api():
    print("do an external api call")
    return True

def get_observation_data():
    return "observation data"

def give_the_user_observation_data():
    try:
        is_allowed = my_new_validation_logic_to_external_api()
        if not is_allowed:
            logger.warn("for user with id x we get not allowed back")
            is_allowed = True
    except Exception as exc:
        logger.warn("We got the following exception: %s", str(exc))
        is_allowed = True

        
    if is_allowed:
        return get_observation_data()
```

An example where you would like to do this for a research project might be when with reinforcement learning steps take too long. This can mean that for cost efficiency at that moment it is the most cost-effective. More information on runtime testing can be found at [the turing way](https://book.the-turing-way.org/reproducible-research/testing/testing-runtime).

# 7. Closing words

In the previous parts we have looked at quite a few different types of test with examples. Also, some ways on making the tests more reusable and improving the quality. We would like to end with giving a few more possible resources where you could find information about different types of tests or testing tools:

- [pytest and all types of integrations with it](https://pytest-with-eric.com/)
- [the turing way](https://book.the-turing-way.org/reproducible-research/testing)
- [Behaviour driven development with Gherkin syntax](https://behave.readthedocs.io/en/latest/tutorial/)
- [testing pyramid vs honeycomb testing](https://engineering.atspotify.com/2018/01/testing-of-microservices/)