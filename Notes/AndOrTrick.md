### Трюк с and-or

Из значений, перечисленных в операторе `or` выбирается первое, выдающее истину (либо самое последнее).

```python
var1 = None
var2 = ''
var3 = 'Text'
result = var1 or var2 or var3
```
В `result` будет помещено `Text`. Также можно сделать так:

```python
def throw_value_error():
    raise ValueError('Bad value detected')
    
var1 = None
var2 = ''    
result = var1 or var2 or throw_value_error()
```
Будет выброшено исключение.

Из значений, перечисленных в операторе `and`:
* Если первое значение выдало истину, выбирается второе.
* Если первое значение выдало ложь, выбирается оно (вот так нетривиально!).

В сочетании с `or` это даёт возможность написать:

```python
a = 1
b = 2
c = 3
result = a and b or c
```
В `result` будет помещено 2. Однако, если `a` сделать равным 0, то в `result` будет помещено 3. Это происходит потому, что последняя строка эквивалентна `result = (a and b) or c`. Так как выражение в скобках вернуло 0, то оператор `or` выбирает второе значение.
