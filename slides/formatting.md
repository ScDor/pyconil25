# Humanize

display human-readable relative time

```
Input: now - 90 seconds
```

<v-clicks>

````md magic-move

```python
import datetime as dt
ago = dt.datetime.now() - dt.timedelta(seconds=90)
delta = dt.datetime.now() - ago
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
import datetime as dt
ago = dt.datetime.now() - dt.timedelta(seconds=90)
print(humanize.naturaltime(ago, minimum_unit="minutes"))
```
````

</v-clicks>

```
Output: a minute ago
```

---

# Unidecode

transliterate accented characters to ASCII

```
Input: àéîõü
```

<v-clicks>

````md magic-move

```python
import unicodedata
s = "àéîõü"
print(unicodedata.normalize('NFKD', s).encode('ascii', 'ignore').decode('ascii'))
```

```python
from unidecode import unidecode
print(unidecode("àéîõü"))
```
````

</v-clicks>

```
Output: aeiou
```

---

# Inflect

pluralize words and generate ordinals

```
Input: file, 7, 10 
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

item = "file"
total = 10
current = 7
print(f"Processing the {ordinal(current)} {plural(item, current)}"
      f"out of {total} {plural(item, total)}")
```

```python
import inflect
p = inflect.engine()
item = "file"
total = 10
current = 7
print(f"Processing the {ordinal(current)} {plural(item, current)}"
      f"out of {total} {plural(item, total)}")
```
````

</v-clicks>

```
Output: Processing the 7th file out of 10 files
```
