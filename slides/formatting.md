---

## Formatting String Modifiers
<v-clicks>
```python
value = 42
print(f"{value:<5}")     # '42   ' (left-align in width 5)
print(f"{value:>5}")     # '   42' (right-align)
print(f"{value:^5}")     # ' 42  ' (center)
```

```python
price = 12.3456
print(f"{price:.2f}")      # 12.35  (2 decimal places)
print(f"{price:8.2f}")     # '   12.35' (width 8, 2 decimals)
```

```python
number = 1234567
print(f"{number:,}")       # 1,234,567
print(f"{number:010}")     # 0001234567 (pad with zeros to width 10)
```

```python
title = "Hello"
print(f"{title:-^20}")     # '-------Hello--------' (centered with -)
print(f"{title:.<20}")     # 'Hello...............' (left with dots)

```

</v-clicks>