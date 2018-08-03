### Цикл for

```python
for i in range(3):
  print(i)
else:
  print('Stop')
# 0
# 1
# 2
# Stop
```

При выходе по `break` ветка `else` не срабатывает.

Если итерируемая последовательность меняется в самом цикле, надо делать так:

```python
a=[1,-2,3,-4]
for x in a[:]:
    if x < 0: a.remove(x)
# a=[1,3]    
```