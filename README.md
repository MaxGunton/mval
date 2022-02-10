
# mval
> We all hate errors and debugging!  Save time debugging by using this simple package for validating your inputs, parameters, etc.


Welcome use the functions in here to speed up code development.  

## Install

`pip install git+https://github.com/MaxGunton/mval.git`

## How to use

```python
from typing import Tuple

color = (123, 234, 25777)
# TODO: finish the restriction portion so it works
validate(color, Tuple[int, int, int], "color", lambda x: all([True for i in x if 0<= i <= 255]))
```




    (123, 234, 25777)


