# Collections: defaultdict

Goal: group people by department

```
Input: [("Alice","Eng"), ("Bob","Sales")]
```

<v-clicks>

````md magic-move

```python
people = [("Alice","Eng"),("Bob","Sales")]
groups = {}
for name, dept in people:
    if dept not in groups:
        groups[dept] = []
    groups[dept].append(name)
print(groups)
```

```python
from collections import defaultdict

groups = defaultdict(list)
people = [("Alice","Eng"),("Bob","Sales")]
for name, dept in people:
    groups[dept].append(name)
print(groups)
```
````

</v-clicks>

```
Output: {'Eng': ['Alice'], 'Sales': ['Bob']}
```
