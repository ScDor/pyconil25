# TQDM

Goal: show progress while iterating steps

```
Input: range(5)
```

<v-clicks>

````md magic-move

```python
import time
total = 5
for i in range(total):
    print("\rProgress: [{}{}] {:>3}%".format(
        "#" * (i+1), 
        "." * (total - i - 1),
         int((i+1)/total*100)
        ), 
        end="",
        flush=True)
    time.sleep(0.5)
```

```python
from tqdm import tqdm
import time
for i in tqdm(range(5)):
    time.sleep(0.5)
```
````

</v-clicks>

```
Outputs: 
Progress: [###..] 60%
60%|█████████████         | 3/5 [00:01<00:01,  2.00it/s]
```
