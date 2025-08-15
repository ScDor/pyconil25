---
    
## Itertools: cycle

```python
from itertools import cycle

count = 0
for item in cycle(['A', 'B', 'C']):
    print(item)
    count += 1
    if count == 6:
        break
```

---

## Itertools: Distinct Combinations

<v-clicks>
```python
import itertools

data = [1, 1, 2, 2]
seen = set()
unique_combos = []

for combo in itertools.combinations(data, 2):
    if combo not in seen:
        seen.add(combo)
        unique_combos.append(combo)
print(unique_combos)
```

<br>
```python
from more_itertools import distinct_combinations
data = [1, 1, 2, 2]
for combo in distinct_combinations(data, 2):
    print(combo)
# Output: (1, 1), (1, 2), (2, 2)

```
</v-clicks>

---

## Itertools: chain

<v-clicks>
```python
a = [1, 2]
b = [3, 4]
c = [5, 6]

combined = []
for x in a:
    combined.append(x)
for x in b:
    combined.append(x)
for x in c:
    combined.append(x)
```

```python
from itertools import chain

result_1 = list(chain(a,b,c))
result_2 = list(chain.from_iterable([a,b,c]))
```

</v-clicks>