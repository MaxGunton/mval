# mval
> We all hate errors and debugging!  Save time debugging by using this simple package for validating your inputs, parameters, etc.


Use the validate_param function to speed up code development.  

## Install

`pip install git+https://github.com/MaxGunton/mval.git`

## How to use

```
from mval import validate_param
from typing import Tuple

good_color = (123, 234, 25)
bad_type_in_color = (28, "hello", 34)
bad_value_in_color = (28738, 75, 34)
good_color2 = (00000000, 43, 23)

def rgb_restr(x):
    try:
        validate_param(x[0], int, "color[0]", "[0,255]")
        validate_param(x[1], int, "color[0]", "[0,255]")
        validate_param(x[2], int, "color[0]", "[0,255]")
    except ValueError as error:
        return False
    return True
```

```
validate_param(good_color, Tuple[int, int, int], "color", p_restrictions=rgb_restr)
```




    (123, 234, 25)



```
try:
    validate_param(bad_type_in_color, Tuple[int, int, int], "color", p_restrictions=rgb_restr)
except TypeError as error:
    print(error)
```

    color expected type typing.Tuple[int, int, int], but received (28, 'hello', 34) of type <class 'tuple'>
    

```
try:
    validate_param(bad_value_in_color, Tuple[int, int, int], "color", p_restrictions=rgb_restr)
except ValueError as error:
    print(error)
```

    (28738, 75, 34) doesn't meet the restrictions enforced by function: <function rgb_restr at 0x7f79d72a5dd0>
    

```
validate_param(good_color2, Tuple[int, int, int], "color", p_restrictions=rgb_restr)
```




    (0, 43, 23)



## TODO

1. Add write up on bounds expression  
    `( means greater than` ***AND*** `[ means greater than or equal to`
    
    `) means less than` ***AND***  `] means less than or equal to`
2. Add write up on how to define functions
