# Typer

Goal: greet a user multiple times from CLI
<!-- 
typer makes it easy to just plug on an existing app, with less boilerplate code
supports shell autocomplete, multiple commands, rich output, ... 
 -->
<v-clicks>

````md magic-move
```python
import argparse

def main():
    p = argparse.ArgumentParser()
    p.add_argument("name")
    p.add_argument("--times", type=int, default=1)
    args = p.parse_args()

    for _ in range(args.times):
        print(f"Hello {args.name}")

if __name__ == "__main__":
    main()
```

```python
import typer

def main(name: str, times: int = 1):
    for _ in range(times):
        print(f"Hello {name}")

if __name__ == "__main__":
    typer.run(main)
```
````
</v-clicks>
