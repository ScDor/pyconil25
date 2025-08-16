# Pathlib

Goal: inspect file parts and build a path

```
Inputs: file=/home/user/docs/report.pdf, folder=/home/user
```

````md magic-move

```python
import os

filepath = "/home/user/docs/report.pdf"
filename = os.path.basename(filepath)
stem, ext = os.path.splitext(filename)
parent = os.path.dirname(filepath)

print(filename, stem, ext, parent)

folder = "/home/user"
full_path = os.path.join(folder, "docs", "report.pdf")
print(full_path)
```


```python
from pathlib import Path

file = Path("/home/user/docs/report.pdf")

print(file.name, file.stem, file.suffix, file.parent)

folder = Path("/home/user")
print(folder / "docs" / "report.pdf")
```
````

```
Output:
report.pdf    report      .pdf      /home/user/docs      /home/user/docs/report.pdf
```
