# Stringy paths are so 2013

```python
my_file = "/home/user/docs/report.pdf"
folder = "/home/user"
```


<v-click>
````md magic-move

```python{|3|3,4|5|8|11|}
import os

filename = os.path.basename(my_file)
stem, ext = os.path.splitext(filename)
parent = os.path.dirname(my_file)
print(filename, stem, ext, parent)

new_path = os.path.join(parent, stem + ".txt")
print(new_path)

full_path = os.path.join(folder, "other_docs", "other_report.pdf")
print(full_path)
```

```python{1|3|3-4|6|8|}
from pathlib import Path

path = Path(my_file)
print(path.name, path.stem, path.suffix, path.parent)

print(str(path.with_suffix(".txt")))

other_path = Path(folder) / "docs" / "other_report.pdf"
print(str(other_path))
```
````

</v-click>
```python
report.pdf    report    .pdf    /home/user/docs
/home/user/docs/report.txt
/home/user/other_docs/other_report.pdf
```
