## Collections: defaultdict

<v-clicks>

```python
people = [ ("Alice", "Engineering"), ("Bob", "Sales"), 
           ("Charlie", "Engineering"), ("David", "Something") ]

groups = {}
for name, department in people:
    if department not in groups:
        groups[department] = []
    groups[department].append(name)
```
<br>
```python
from collections import defaultdict
groups = defaultdict(list)

for name, dept in people:
    groups[dept].append(name)
```
</v-clicks>

---

## Collections: namedtuple

<v-clicks>

```python
def get_point():
    return (3, 4)
point = get_point()
print(f"x: {point[0]}, y: {point[1]}")  # Confusing!
```

```python
from collections import namedtuple
Point = namedtuple('Point', ['x', 'y'])
p = Point(3, 4)
print(f"x: {point.x}, y: {point.y}") 

```

```python
from typing import NamedTuple

class Point(NamedTuple):
    x: float
    y: float

p = Point(3, 4)
print(p)    # Point(x=3,y=4)
```

</v-clicks>

---

### namedtuple vs @dataclass


|                 | `namedtuple`       | `@dataclass`                          |
|-----------------------|--------------------------------------|----------------------------------------|
| Mutability            | Immutable (by default)               | Mutable (unless `frozen=True`)         |
| Type hints            | ✅ with `typing.NamedTuple`          | ✅ Native support                      |
| Performance           | Slightly faster                      | Slightly slower, but negligible       |
| Comparable | ✅ | ❌ |
| Hashable | ✅ | ❌ |
| Iterable | ✅ | ❌ |