# Pathlib 
<v-clicks>

```python
import os

filepath = "/home/user/documents/report.pdf"
filename = os.path.basename(filepath)

```

```python
from pathlib import Path

filepath = Path("/home/user/documents/report.pdf")
filename = filepath.name

print(filename)          # report.pdf
print(filepath.stem)     # report
print(filepath.suffix)   # .pdf
print(filepath.parent)   # /home/user/documents
```

```python
folder = Path("/home/user")
full_path = folder / "documents" / "report.pdf"

```

</v-clicks>