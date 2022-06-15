# mval
> Simple package for validating your input parameters.


We all hate errors and debugging, save time debugging by FAILING FAST and having SINGLE SOURCES using the following functions:

[validate_param](core.html/#validate_param): check user passed variables to ensure they meet set of requirements. (FAST FAIL idealogy)

[documented_by](core.html/#documented_by): copy docstring a function, intended for wrapper functions and decorators. (SINGLE SOURCE idealogy)

## Install

`pip install git+https://github.com/MaxGunton/mval.git`

## How to use

**For example:**

Assume we want to get some user input, and it needs to be a color represented by a tuple of 3 integers ranging from 0 to 255 inclusive.  We could write a function to do this that raises an exception if the value is bad, but it's been done for you!

```python
from typing import Tuple, Union, List  # for dictating nested types

# below are a series of possible user inputs some good and some bad
good_color = (123, 234, 25)
bad_type_in_color = (28, "hello", 34)
bad_value_in_color = (28738, 75, 34)
good_color2 = (00000000, 43, 23)

# lets define a functional restriction that returns True if all iteratible values are [0,255] and false otherwise
color_restriction = lambda x: all([True if 0<=i<=255 else False for i in x])
```

```python
# This one should pass and return the original value
validate_param(good_color, Tuple[int, int, int], "color", color_restriction)
```




    (123, 234, 25)



```python
# This one should fail because there is a bad type in the parameter.  This will raise an exception that we can understand
try:
    validate_param(bad_type_in_color, Tuple[int, int, int], "color", color_restriction)
except TypeError as error:
    print(error)
```

    color expected type typing.Tuple[int, int, int], but received (28, 'hello', 34) of type <class 'tuple'>


```python
# Again this one should fail, but because a value in the Tuple is out of range.
try:
    validate_param(bad_value_in_color, Tuple[int, int, int], "color", color_restriction)
except ValueError as error:
    print(error)
```

    (28738, 75, 34) doesn't meet the restrictions enforced by function: <function <lambda> at 0x000002CF8B4AA620>


```python
# This one should pass and return the original value even though it had many leading 0's
validate_param(good_color2, Tuple[int, int, int], "color", color_restriction)
```




    (0, 43, 23)


