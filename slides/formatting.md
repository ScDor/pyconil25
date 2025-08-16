# Humanize

display human-readable relative time

```python
import datetime 
ago = datetime.datetime.now() - datetime.timedelta(seconds=90)
```

<v-clicks>

````md magic-move
```python
delta = datetime.datetime.now() - ago
seconds = int(delta.total_seconds())

if seconds < 60:
    text = f"{seconds} second" + ("s" if seconds != 1 else "") + " ago"
elif seconds < 120:
    text = "a minute ago"
else:
    mins = seconds // 60
    text = f"{mins} minute" + ("s" if mins != 1 else "") + " ago"
print(text)
```

```python
import humanize
print(humanize.naturaltime(ago))
```
````

</v-clicks>

```python
"a minute ago"
```

---

# Inflect

pluralize words and generate ordinals

```python
item = "file"
total = 10
current = 7
```

<v-clicks>

````md magic-move
```python{1-2|4-9|11-15}
def plural(word: str, count: int) -> str:
    return word + ("s" if count != 1 else "")

def ordinal(n: int) -> str:
    if 11 <= (n % 100) <= 13:
        suffix = "th"
    else:
        suffix = ["th", "st", "nd", "rd", "th"][min(n % 10, 4)]
    return str(n) + suffix
    print(f"Processing the {ordinal(current)} {plural(item, current)}"
          f"out of {total} {plural(item, total)}")

```

```python
import inflect
p = inflect.engine()
print(f"Processing the {p.ordinal(current)} {p.plural(item, current)}"
      f"out of {total} {p.plural(item, total)}")
```
````

</v-clicks>

```python
>>> "Processing the 7th file out of 10 files"
```
