### Распаковка контейнеров

Всем известны следующие трюки:
```python
a, b = 1, 2 # групповое присвоение
b, a = a, b # обмен значениями
```

Но в Python 3 можно написать и так:
```python
a, *b, c = 1, 2, 3, 4, 5
```
В `b` будет помещен кортеж `[2, 3, 4]`.