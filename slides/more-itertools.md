# More-itertools: one

Goal: assert there is exactly one item

```
Input: [42]
```

<v-clicks>

````md magic-move

```python
items = [42]
if len(items) != 1:
    raise ValueError("Expected exactly one item")
item = items[0]
print(item)
```

```python
from more_itertools import one
print(one([42]))
```
````

</v-clicks>

```
Output: 42
```

---

# More-itertools: map_reduce

Goal: group items by an uppercase key

```
Input: "abbccc"
```

<v-clicks>

````md magic-move

```python
from collections import defaultdict

grouped = defaultdict(list)
for item in "abbccc":
    grouped[item.upper()].append(item)
print(dict(grouped))
```

```python
from more_itertools import map_reduce
print(map_reduce("abbccc", keyfunc=str.upper))
```
````

</v-clicks>

```
Output: {'A': ['a'], 'B': ['b', 'b'], 'C': ['c', 'c', 'c']}
```

---

# More-itertools: always_iterable

Goal: iterate over a single value or list uniformly

```
Input: "alice", ["bob", "carol"], None
```

<v-clicks>

````md magic-move

```python
def greet(users):
    if users is None:
        return
    if isinstance(users, str):
        users = [users]
    for u in users:
        print(f"Hello {u}")

greet("alice")
greet(["bob","carol"])
greet(None)
```

```python
from more_itertools import always_iterable

def greet(users):
    for u in always_iterable(users, base_type=str):
        print(f"Hello {u}")

greet("alice")
greet(["bob","carol"])
greet(None)
```
````

</v-clicks>

```
Output:
Hello alice
Hello bob
Hello carol
```

---

# More-itertools: chunked

Goal: split an iterable into fixed-size chunks

```
Input: range(7), size=3
```

<v-clicks>

````md magic-move

```python
data = list(range(7))
size = 3
chunks = [data[i:i+size] for i in range(0, len(data), size)]
print(chunks)
```

```python
from more_itertools import chunked
print(list(chunked(range(7), 3)))
```
````

</v-clicks>

```
Output: [[0, 1, 2], [3, 4, 5], [6]]
```

---

# More-itertools: partition

Goal: partition an iterable by a predicate

```
Input: range(10)
```

<v-clicks>

````md magic-move

```python
data = list(range(10))
odds = [x for x in data if x % 2]
evens = [x for x in data if not x % 2]
print(odds)
print(evens)
```

```python
from more_itertools import partition
odds, evens = partition(lambda x: x % 2, range(10))
print(list(odds))
print(list(evens))
```
````

</v-clicks>

```
Output:
[1, 3, 5, 7, 9]
[0, 2, 4, 6, 8]
```
