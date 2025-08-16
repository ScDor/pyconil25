# Boltons: args2cmd / args2sh

Goal: render args as a command and a shell-quoted string

```
Input: ["python", "my script.py", "--name", "O'Reilly & Co."]
```

<v-clicks>

````md magic-move

```python
import shlex

args = ["python", "my script.py", "--name", "O'Reilly & Co."]

print(" ".join(shlex.quote(a) for a in args))
print(" ".join(f"'{a}'" for a in args))
```

```python
from boltons.strutils import args2cmd, args2sh

args = ["python", "my script.py", "--name", "O'Reilly & Co."]

print(args2cmd(args))
print(args2sh(args))
```
````

</v-clicks>

```
Outputs:
python "my script.py" --name "O'Reilly & Co."
'python' 'my script.py' '--name' 'O'\''Reilly & Co.'
```

---

# Boltons: MultiReplace

Goal: replace multiple substrings efficiently

```
Input: "I love python and rust"
```

<v-clicks>

````md magic-move
```python
text = "I love python and rust"
mapping = {"py": "🐍", "rust": "🦀"}

for k, v in mapping.items():
    text = text.replace(k, v)
print(text)
```

```python
from boltons.strutils import MultiReplace

replacer = MultiReplace({"py": "🐍", "rust": "🦀"})
print(replacer("I love python and rust"))
```
````

</v-clicks>

```
Output: I love 🐍thon and 🦀
```

---

# Boltons: daterange

Goal: iterate dates in a half-open range

```
Input: start=2025-01-01, end=2025-01-05
```

<v-clicks>

````md magic-move

```python
from datetime import date, timedelta

start, end = date(2025,1,1), date(2025,1,5)
cur = start
while cur < end:
    print(cur)
    cur += timedelta(days=1)
```

```python
from boltons.timeutils import daterange
from datetime import date

for d in daterange(date(2025,1,1), date(2025,1,5)):
    print(d)
```
````

</v-clicks>

```
Outputs:
2025-01-01
2025-01-02
2025-01-03
2025-01-04
```

---

# Boltons: bytes2human

Goal: format bytes into a human-readable string

```
Input: 12345678
```

<v-clicks>

````md magic-move

```python
size = 12345678
units = ["", "K", "M", "G", "T"]
idx = 0
while size >= 1024 and idx < len(units)-1:
    size /= 1024
    idx += 1
print(f"{size:.1f}{units[idx]}")
```

```python
from boltons.strutils import bytes2human
print(bytes2human(12345678, 2)) # 2 decimal places
```
````

</v-clicks>

```
Output: 11.77M
```

---
# Boltons: `cardinalize`

**Goal:** Conditionally pluralize a word based on count, with case preserved.  

```
Input: (5, "vowel")  
Input: (3, "Wish")
```

<v-clicks>

````md magic-move
```python
def pluralize(word, count):
    if count == 1:
        return word
    return word + "s"

vowels = 'aeiou'

print(len(vowels), pluralize("vowel", len(vowels)))
print(3, pluralize("Wish", 3))
```

```python
from boltons.strutils import cardinalize

vowels = 'aeiou'

print(len(vowels), cardinalize('vowel', len(vowels)))
print(3, cardinalize('Wish', 3))
```
````

</v-clicks>

```
Outputs:
5 vowels
3 Wishs        # wrong
5 vowels
3 Wishes       # correct
```

