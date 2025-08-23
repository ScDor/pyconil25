# More-itertools: one

<!-- We won't cover excellent itertools today, but its extension -->
Assert there is exactly one item, and get its value

```python
items = [42]
```
<v-clicks>

````md magic-move

```python
if len(items) != 1:
    raise ValueError("Expected exactly one item")

print(items[0])
```
```python
from more_itertools import one
print(one(items))
```
````
</v-clicks>
<!-- 
exception for too many/little are customizable.
good in tests 
 -->

```
42
```

---

# More-itertools: map_reduce

group items by an uppercase key

```python
items = "abbccc"
```

<v-clicks>

````md magic-move

```python
grouped = dict()

for item in items:
    key = item.upper()
    if key in grouped:
        grouped[key].append(item)
    else:
        grouped[key] = [item]

```

```python
from collections import defaultdict

grouped = defaultdict(list)

for item in items:
    grouped[item.upper()].append(item)
```
```python
from more_itertools import map_reduce
grouped = map_reduce(items, keyfunc=str.upper)
```
````

</v-clicks>

```python
print(dict(grouped))
>>> {'A': ['a'], 'B': ['b', 'b'], 'C': ['c', 'c', 'c']}
```

<!-- here we see the tradeoff, may take a moment to understand always_iterable, but if the team adapts, everybody wins -->

---

# More-itertools: always_iterable

iterate over a single value or list uniformly

<v-clicks>

````md magic-move

```python
def greet(users: str | Iterable[str] | None):
    if users is None:
        return

    if isinstance(users, str):
        users = [users]

    for user in users:
        print(f"Hello {user}")
```

```python
from more_itertools import always_iterable

def greet(users: str | Iterable[str] | None):
    for user in always_iterable(users):
        print(f"Hello {user}")
```
````

</v-clicks>

```python
greet("Alice")
greet(["Bob","Carol"])
greet(None)

>>> Hello Alice
>>> Hello Bob
>>> Hello Carol
```

---

# More-itertools: chunked
<!-- a common example for snippets from GPT/StackOverflow -->
split an iterable into fixed-size chunks

<v-clicks>

````md magic-move

```python
def chunk_things(iterable: list[int], chunk_size: int) -> list[int]:
    return [data[i : i + chunk_size] for i in range(0, len(data), chunk_size)]
```


```python
from more_itertools import chunked
list(chunked(range(7), 3))
```
````

</v-clicks>

```python
chunk_things(range(7), 3)
>>> [[0, 1, 2], [3, 4, 5], [6]]
```

---

# More-itertools: partition

partition an iterable by a predicate

```python
numbers = range(10)
```
<v-clicks>

````md magic-move

```python
data = list(numbers)
odds = [x for x in data if x % 2]
evens = [x for x in data if not x % 2]
```

```python
from more_itertools import partition
odds, evens = partition(lambda x: x % 2, numbers)
```
````

</v-clicks>

```python
print(odds)
print(evens)
[1, 3, 5, 7, 9]
[0, 2, 4, 6, 8]
```
