# Dunder `__bool__`

-----

Used for built-in **truth** value testing and invoked by the builtin `bool(...)` method.  This method
should return either `False` or `True` booleans respectively and if a dunder `__bool__` is omitted from
a class, instances of such class will be checked based on a `__len__`.  In the event that `__len__` exists,
anything other than nonzero is considered `True`.  If neither a `__bool__` or `__len__` are defined, instances
of such classes are determined to be `True` in a boolean context.`

-----

### Examples

User defined classes by default will return `True` when evaluated in a boolean context.  This is because
neither `__bool__` or `__len__` are defined.

```py title="Default User Defined Objects" linenums="1"
class Default:
    ...

bool(Default())  # True
```

In order to override the boolean behaviour, implement `__bool__` and return `True`|`False` accordingly.
```py title="Custom dunder bool", linenums="1" hl_lines="6 7"
class DunderBool:
    
    def __init__(self, x: int) -> None:
        self.x = x
        
    def __bool__(self) -> bool:
        return self.x > 100
        
bool(DunderBool(100))  # False
bool(DunderBool(101))  # True
```

If `__len__` is implemented and `__bool_` is not, `__len__` is used as a fallback, where non-zero values
are considered `True`.

```py title="Fallback to __len__", linenums="1" hl_lines="9 10"
from typing import Optional
from typing import List

class FallbackToLen:

    def __init__(self, container: Optional[List[int]] = None) -> None:
        self.container = container or []

    def __len__(self) -> int:
        return len(self.container)

bool(FallbackToLen([1]))  # True
bool(FallbackToLen()) # False
```

-----

#### Python Docs

[Read More :fontawesome-solid-paper-plane:](https://docs.python.org/3/reference/datamodel.html#object.__bool__){ .md-button .md-button--primary }
