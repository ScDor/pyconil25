---

# Boltons: `bytes2human`

format bytes into a human-readable string

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

