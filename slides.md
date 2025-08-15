---
theme: seriph
background: https://i.ibb.co/khMnPgg/killarney.jpg
title: Write Less Code
info: Dor Schwartz @ PyCon AT 2025
drawings:
    persist: true
transition: fade
hideInToc: true
layout: cover
colorSchema: light
---
<style>
.slidev-code {
  --slidev-code-font-size: 16px; 
  font-size: var(--slidev-code-font-size) !important;
}
</style>
 
 # Write Less Code

Dor Schwartz @ PyCon Austria 2025

---

 
 
  
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


---

# Pathlib 
<v-clicks>

```python
import os

filepath = "/home/user/documents/report.pdf"
filename = os.path.basename(filepath)

```

```python
from pathlib import Path

filepath = Path("/home/user/documents/report.pdf")
filename = filepath.name

print(filename)          # report.pdf
print(filepath.stem)     # report
print(filepath.suffix)   # .pdf
print(filepath.parent)   # /home/user/documents
```

```python
folder = Path("/home/user")
full_path = folder / "documents" / "report.pdf"

```

</v-clicks>




---

## More-itertools: one

<v-clicks>

```python
items = [42]

if len(items) != 1:
    raise ValueError("Expected exactly one item")

item = items[0]
```


```python
from more_itertools import one

item = one([42])  # Raises ValueError if not exactly one item

```

```python 
>> one(["🐍","🦀"])  

Traceback (most recent call last):
ValueError: too many items in iterable (expected 1)'

>> one([], too_short=IndexError('too few items'))
Traceback (most recent call last):
IndexError: too few items
```

</v-clicks>

---

## More-itertools: map_reduce

<v-clicks>

```python
from collections import defaultdict

keyfunc = lambda x: x.upper()
grouped = defaultdict(list)

for item in 'abbccc':
    key = keyfunc(item)
    grouped[key].append(item)

result = dict(grouped)

# {'A': ['a'], 'B': ['b', 'b'], 'C': ['c', 'c', 'c']}

```
<br>

```python
from more_itertools import map_reduce

result = map_reduce('abbccc', keyfunc=lambda x: x.upper())
# {'A': ['a'], 'B': ['b', 'b'], 'C': ['c', 'c', 'c']}

```

</v-clicks>


---

## More-itertools: always_iterable

<v-clicks>

```python
def greet_users(usernames: str | Iterable[str] | None):
    if usernames is None:
        return
    if isinstance(usernames, str):
        usernames = [usernames]
    for name in usernames:
        print(f"Hello {name}")

greet_users("alice")
greet_users(["bob", "carol"])
greet_users(None)
```
<br>

```python
from more_itertools import always_iterable

def greet_users(usernames: str | Iterable[str] | None):
    for name in always_iterable(usernames, base_type=str):
        print(f"Hello {name}")

```

</v-clicks>


---

## More-itertools: Partition

<v-clicks>

```python
evens, odds = [], []

for i in range(10):
    if i % 2 == 0:
        evens.append(i)
    else:
        odds.append(i)

print(evens, odds)
```
<br>
```python
from more_itertools import partition

odds, evens = partition(lambda x: x % 2, range(10))

print(list(evens), list(odds))
```

</v-clicks>

---

## More-itertools: chunks

<v-clicks>

```python
def chunks(seq, size):
    return [seq[i:i + size] for i in range(0, len(seq), size)]

print(chunks([1, 2, 3, 4, 5], 2))
```
<br>

```python
from more_itertools import chunked

print(list(chunked([1, 2, 3, 4, 5], 2)))
# Output: [[1, 2], [3, 4], [5]]```
```

</v-clicks>

---

## More-itertools: window

<v-clicks>

```python
def sliding_window(seq, n):
    return [tuple(seq[i:i+n]) for i in range(len(seq) - n + 1)]

print(sliding_window([1, 2, 3, 4], 2))
```
<br>

```python
from more_itertools import windowed

print(list(windowed([1, 2, 3, 4], 2)))
# Output: [(1, 2), (2, 3), (3, 4)]

```

</v-clicks>


---

    
## Itertools: cycle

```python
from itertools import cycle

count = 0
for item in cycle(['A', 'B', 'C']):
    print(item)
    count += 1
    if count == 6:
        break
```

---

## Itertools: Distinct Combinations

<v-clicks>
```python
import itertools

data = [1, 1, 2, 2]
seen = set()
unique_combos = []

for combo in itertools.combinations(data, 2):
    if combo not in seen:
        seen.add(combo)
        unique_combos.append(combo)
print(unique_combos)
```

<br>
```python
from more_itertools import distinct_combinations
data = [1, 1, 2, 2]
for combo in distinct_combinations(data, 2):
    print(combo)
# Output: (1, 1), (1, 2), (2, 2)

```
</v-clicks>

---

## Itertools: chain

<v-clicks>
```python
a = [1, 2]
b = [3, 4]
c = [5, 6]

combined = []
for x in a:
    combined.append(x)
for x in b:
    combined.append(x)
for x in c:
    combined.append(x)
```

```python
from itertools import chain

result_1 = list(chain(a,b,c))
result_2 = list(chain.from_iterable([a,b,c]))
```

</v-clicks>

---

## Pydantic Settings

```python
from pydantic_settings import BaseSettings
from pydantic import Field, SecretStr

class UserSettings(BaseSettings):
    user: str
    password: SecretStr

class Settings(BaseSettings):
    app_name: str = "My Cool App"
    debug: bool = Field(default=False, env="DEBUG")
    port: int = 8000
    user: UserSettings
    class Config:
        env_file = ".env"  # optional
...

settings = Settings()
print(settings.app_name)
print(settings.debug)
```

---

## Formatting String Modifiers
<v-clicks>
```python
value = 42
print(f"{value:<5}")     # '42   ' (left-align in width 5)
print(f"{value:>5}")     # '   42' (right-align)
print(f"{value:^5}")     # ' 42  ' (center)
```

```python
price = 12.3456
print(f"{price:.2f}")      # 12.35  (2 decimal places)
print(f"{price:8.2f}")     # '   12.35' (width 8, 2 decimals)
```

```python
number = 1234567
print(f"{number:,}")       # 1,234,567
print(f"{number:010}")     # 0001234567 (pad with zeros to width 10)
```

```python
title = "Hello"
print(f"{title:-^20}")     # '-------Hello--------' (centered with -)
print(f"{title:.<20}")     # 'Hello...............' (left with dots)

```

</v-clicks>

---
layout: cover
background: https://i.ibb.co/khMnPgg/killarney.jpg
hideInToc: true
---
# Thank you

<br>

## [/in/dor-schwartz](https://www.linkedin.com/in/dor-schwartz/)

