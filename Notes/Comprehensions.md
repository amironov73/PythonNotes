### Генераторы

#### Генератор списков

```python
numbers = [1, 2, 3, 4, 5]
squares = [x * x for x in numbers] # [1, 4, 9, 16, 25]
squares2 = [x * x for x in numbers if x % 2 == 1] # [1, 9, 25]
```

Можно генерировать списки по двум и более последовательностям:

```python
[(x, y, x * y) for x in range(10) for y in range(10) if x < y]
```

#### Выражения-генераторы

```python
squares = (x * x for x in range(10))
for n in squares:
    print(n, end=',')
# 0,1,4,9,16,25,36,49,64,81,    
```
