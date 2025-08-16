# Pathlib

inspect file parts and build a path

```python
my_file = "/home/user/docs/report.pdf"
folder = "/home/user"
```


<v-click>
````md magic-move

```python{|3|3,4|5|8|}
import os

filename = os.path.basename(my_file)
stem, ext = os.path.splitext(filename)
parent = os.path.dirname(my_file)
print(filename, stem, ext, parent)

full_path = os.path.join(folder, "docs", "other_report.pdf")
print(full_path)
```

```python
from pathlib import Path

path = Path(my_file)
print(path.name, path.stem, path.suffix, path.parent)

other_path = Path(folder) / "docs" / "other_report.pdf"
print(str(other_path))
```
````

</v-click>
```python
report.pdf    report    .pdf    /home/user/docs    /home/user/docs/other_report.pdf
```
