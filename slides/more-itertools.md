---


# Bite-sized data

<!-- We won't cover excellent itertools today, but its extension -->
<!-- a common example for snippets from GPT/StackOverflow -->

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

# Group(ing) Therapy

```python
numbers = range(6)
```

<v-clicks>

````md magic-move

```python
grouped = dict()

for num in numbers:
    key = num % 3
    if key in grouped:
        grouped[key].append(num)
    else:
        grouped[key] = [num]

```

```python
from collections import defaultdict

grouped = defaultdict(list)

for num in numbers:
    grouped[num % 3].append(num)
```
```python
from more_itertools import map_reduce
grouped = map_reduce(numbers, keyfunc=lambda num: num % 3)
```
````
</v-clicks>

```python
print(dict(grouped))
>>> {
        0: [0, 3],
        1: [1, 4],
        2: [2, 5]
    }
```


---

# You're an iterable, Harry

<!--
here we see the tradeoff, may take a moment to understand always_iterable, but if the team adapts, everybody wins.
Saving the headache of edge cases
-->


<v-clicks>

````md magic-move

```python
def greet(users: str | Iterable[str] | None):
    if users is None:
        return

    if not isinstance(users, list):
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