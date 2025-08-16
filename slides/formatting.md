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

def pluralize(word: str, count:int) -> str:
    return word+"s" if count > 1 else word

if seconds < 60:
    text = f"{seconds} {pluralize("second", seconds)} ago"
elif seconds < 120:
    text = "a minute ago"
elif seconds < 3600:
    mins = seconds // 60
    text = f"{mins} {pluralize("minute", mins)} ago"
else:
    hours = seconds // 3600
    text = f"{hours} {pluralize("hour", hours)} ago"
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