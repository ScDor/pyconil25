# Questionary

prompt the user to select an option

```
Input: Choose a color [red/blue/green]
```

<v-clicks>

````md magic-move

```python
choice = input("Choose a color [red/blue/green]: ")
print(choice)
```

```python
import questionary
color = questionary.select(
    "Choose a color",
    choices=["red","blue","green"]
).ask()
print(color)

```
```python
import questionary
color = questionary.select(
    "Choose a color",
    choices=["red","blue","green"]
).ask()
print(color)

> ? Choose a color (Use arrow keys)
> » red
>   blue
>   green

```
````

</v-clicks>

```
Output: red
```
