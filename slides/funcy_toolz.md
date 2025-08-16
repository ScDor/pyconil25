# Funcy / Toolz

compose simple string transforms

```
Input: " Hello "
```

<v-clicks>

````md magic-move

```python
def strip_and_lower(s):
    return str.lower(str.strip(s))
print(strip_and_lower(" Hello "))
```

```python
from funcy import compose
strip_and_lower = compose(str.strip, str.lower)
print(strip_and_lower(" Hello "))
```
````

</v-clicks>

```
Output: hello
```

---

create a pre-filled function (partial application)

```
Input: add5(10)
```

<v-clicks>

````md magic-move

```python
def add(x, y):
    return x + y
def add5(y):
    return add(5, y)
print(add5(10))
```

```python
from toolz import curry

@curry
def add(x, y):
    return x + y
add5 = add(5)
print(add5(10))
```
````

</v-clicks>

```
Output: 15
```
