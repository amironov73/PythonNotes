### Словари

Создание словаря с помощью именованных аргументов:

```python
d = dict(a=1, b=2, c=3)
# {'a': 1, 'b': 2, 'c': 3}
```

Преобразование словаря в список:

```python
dictionary = {'a': 1, 'b': 2, 'c': 3}
dict_as_list = dictionary.items()
# [('a', 1), ('b', 2), ('c', 3)] 
```

Преобразование списка в словарь:

```python
mylist = [['a', 1], ['b', 2], ['c', 3]]
dictionary = dict(mylist)
# dictionary = {'a': 1, 'b': 2, 'c': 3} 
```

Генерация словаря по-старому:

```python
d = dict([i, 'N' + str(i)] for i in range(10))
# {0: 'N0', 1: 'N1', 2: 'N2', 3: 'N3', 4: 'N4', 
# 5: 'N5', 6: 'N6', 7: 'N7', 8: 'N8', 9: 'N9'}
```

Генерация словаря по-новому (в Python 3):

```python
d = { i: 'N' + str(i) for i in range(10) }
# результат тот же
```

#### defaultdict

Это словарь, во всем аналогичный простому dict, кроме одного: если в словаре нет искомого ключа, он вызывает заданную функцию и возвращает ее результат. Это позволяет не проверять наличие ключа перед обращением к словарю.

```python
import collections

d = collections.defaultdict(int)
d['red'] += 1
d['blue'] += 1
d['red'] += 1
print(sorted(d.items()))
# [('blue', 1), ('red', 2)]
```

Для работы со списками по ключу отлично подходит `defaultdict(list)`:

```python
import collections

d = collections.defaultdict(list)
d['red'].append('apple')
d['blue'].append('sky')
d['blue'].append('water')
print(sorted(d.items()))
# [('blue', ['sky', 'water']), ('red', ['apple'])]
```

Для `defaultdict(int)` заведен специальное класс `Counter`:

```python
import collections

d = collections.Counter()
d['beer'] += 1
d['steak'] += 2
d['wine'] += 2
print(sorted(d.items()))
# [('beer', 1), ('steak', 2), ('wine', 2)]
```

#### Слияние двух словарей

В Python 3.5 и выше:

```python
x = { 'one': 'two', 'three' : 'four' }
y = { 'five': 'six', 'one': 'eight' }
z = { **x, **y }
# z = {'one': 'eight', 'three': 'four', 'five': 'six'}
```
Раньше:

```python
x = { 'one': 'two', 'three' : 'four' }
y = { 'five': 'six', 'one': 'eight' }
z = x.copy().update(y)
# результат тот же
```

#### Как отсортировать словарь по значениям

```python
import operator

x = {1: 2, 3: 4, 4: 3, 2: 1, 0: 0}
sorted_x = sorted(x.items(), key=operator.itemgetter(1))
# sorted_x = [(0, 0), (2, 1), (1, 2), (4, 3), (3, 4)]
```

или так:

```python
x = {1: 2, 3: 4, 4: 3, 2: 1, 0: 0}
for w in sorted(x, key=x.get, reverse=True):
  print(w, x[w])
# 3 4
# 4 3
# 1 2
# 2 1
# 0 0  
```