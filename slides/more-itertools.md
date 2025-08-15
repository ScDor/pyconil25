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