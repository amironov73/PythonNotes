### Модуль itertools

Модуль предоставляет множество инструментов для работы с последовательностями.

* **accumulate(iterable[, func])** - последовательность сумм значений из последовательности. Реализовано примерно так:

```python
import operator

def accumulate(iterable, func=operator.add):
    "Return running totals"
    # accumulate([1,2,3,4,5]) --> 1 3 6 10 15
    # accumulate([1,2,3,4,5], operator.mul) --> 1 2 6 24 120
    it = iter(iterable)
    try:
        total = next(it)
    except StopIteration:
        return
    yield total
    for element in it:
        total = func(total, element)
        yield total
```

Примеры:
```python
import operator
from itertools import accumulate

data = [3, 4, 6, 2, 1, 9, 0, 7, 5, 8]
print(list(accumulate(data, operator.mul)))
# [3, 12, 72, 144, 144, 1296, 0, 0, 0, 0]

print(list(accumulate(data, max)))
# [3, 4, 6, 6, 6, 9, 9, 9, 9, 9]
```

* **chain(\*iterables)** - последовательность последовательностей

* **combinations(iterable, r)** - комбинации элементов

```python
from itertools import combinations
print(list(combinations('ABC', 2)))
# [('A', 'B'), ('A', 'C'), ('B', 'C')]
```

* **combinations_with_replacement(iterable, r)** - комбинации с замещениями

```python
from itertools import combinations
print(list(combinations('ABC', 2)))
# [('A', 'A'), ('A', 'B'), ('A', 'C'), ('B', 'B'), ('B', 'C'), ('C', 'C')]
```

* **compress(data, selectors)** - выбирает из последовательности только те элементы, для которых селекторы выдают `True`:

```python
from itertools import compress
print(list(compress('ABCDEF', [1,0,1,0,1,1])))
# ['A', 'C', 'E', 'F']
``` 

* **count(start=0, step=1)** - выдает бесконечную возрастающую последовательность-счетчик.

* **cycle(iterable)** - циклически повторяет заданную последовательность.

* **dropwhile(predicate, iterable)** - выбрасывает из последовательности первые элементы, удовлетворяющие предикату.

* **filterfalse(predicate, iterable)** - выбирает из последовательности только те элементы, для которых предикат выдает `False`.

* **groupby(iterable, key=None)** - группировка (довольно простая):

```python
from itertools import groupby
chars = 'AAAABBBCCDAABBB'
grouped = groupby(chars)
for k, g in grouped:
  print(k, list(g))
# A ['A', 'A', 'A', 'A']
# B ['B', 'B', 'B']
# C ['C', 'C']
# D ['D']
# A ['A', 'A']
# B ['B', 'B', 'B']
```

* **islice(iterable, stop)**, **islice(iterable, start, stop[, step])** - подпоследовательность из данной последовательности

```python
from itertools import islice
print(list(islice('ABCDEFG', 2)))
# ['A', 'B']

print(list(islice('ABCDEFG', 2, 4)))
# ['C', 'D']

print(list(islice('ABCDEFG', 2, 6, 2)))
# ['C', 'E']
```

* **permutations(iterable, r=None)** - перестановки

```python
from itertools import permutations
print(list(permutations('ABCD', 2)))
# [('A', 'B'), ('A', 'C'), ('A', 'D'), ('B', 'A'), ('B', 'C'), ('B', 'D'),
#  ('C', 'A'), ('C', 'B'), ('C', 'D'), ('D', 'A'), ('D', 'B'), ('D', 'C')]
```
* **product(*iterables, repeat=1)** - перемножение последовательностей

```python
from itertools import product
print(list(product('ABC', 'XYZ')))
# [('A', 'X'), ('A', 'Y'), ('A', 'Z'), ('B', 'X'), ('B', 'Y'), ('B', 'Z'),
#  ('C', 'X'), ('C', 'Y'), ('C', 'Z')]
```

* **repeat(object[, times])** - повторение объекта указанное число раз

* **starmap(function, iterable)** - применение указанной функции к последовательности (аргументы берутся из кортежей в последовательности)

```python
from itertools import starmap
print(list(starmap(pow, [(2,5), (3,2), (10,3)])))
# [32, 9, 1000]
```

* **takewhile(predicate, iterable)** - берет из последовательности только ту часть, начиная с начала, для которой предикат выдает `True`.

* **tee(iterable, n=2)** - запускает n независимых итераторов на данной последовательности

```python
from itertools import tee
for x in tee('ABCDEFGH'):
  print(list(x))
# ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H']
# ['A', 'B', 'C', 'D', 'E', 'F', 'G', 'H']
```

* **zip_longest(\*iterables, fillvalue=None)** - аналогично обычной zip, только недостающие элементы заменяются на `fillvalue`.