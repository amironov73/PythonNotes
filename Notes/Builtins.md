### Встроенные функции

Модуль `builtins` импортируется автоматически и, как правило, нет необходимости импортировать его вручную. Но можно провернуть, например, такой трюк:

```python
import builtins

def open(path):
    f = builtins.open(path, 'r')
    return UpperCaser(f)

class UpperCaser:
    '''Wrapper around a file that converts output to upper-case.'''

    def __init__(self, f):
        self._f = f

    def read(self, count=-1):
        return self._f.read(count).upper()

    # ...
```

#### Функции

* **abs(x)** - работает в т. ч. и для комплексных чисел.

* **all(iterable)** - эквивалентно

```python
def all(iterable):
    for element in iterable:
        if not element:
            return False
    return True
```

* **any(iterable)** - эквивалентно

```python
def any(iterable):
    for element in iterable:
        if element:
            return True
    return False
```

* **ascii(object)** - аналогично `repr`, однако, все не-ASCII символы выводятся с помощью `\x`, `\u` и т. п.


* **bin(x)** - конвертирует целое в битовую строку:

```python
bin(3)
# '0b11'
bin(-10)
# '-0b1010'
```

* **bool(x)** - преобразование любого объекта в булево значение (если возможно)

* **bytearray([source[, encoding[, errors]]])** и **bytes([source[, encoding[, errors]]])** - преобразование последовательности целых в байтовые строки.

* **callable(object)** - определение, является ли объект вызываемым.

* **chr(i)** - символ с указанным кодом.

* **compile(source, filename, mode, flags=0, dont_inherit=False, optimize=-1)** - компилирует переданный код в объект AST.

* **delattr(object, name)** - удаление атрибута у объекта.

* **dir([object])** - получение списка атрибутов у объекта, либо списка имен, доступного в текущем контексте.

* **divmod(a, b)** - вычисление частного и остатка от деления.

* **enumerate(iterable, start=0)** - выдает пары `(индекс, элемент)`. Здесь `start` - индекс, с которого начнется нумерация.

* **eval(expression, globals=None, locals=None)** - вычисление значения выражения.

* **exec(object[, globals[, locals]])** - выполнение кода. Здесь `object` может быть как строкой, так и объектом кода.

* **filter(function, iterable)** - фильтрация последовательности.

* **float([x])** - преобразование объекта в число с плавающей точкой.

* **format(value[, format_spec])** - форматирование объекта.

* **frozenset([iterable])** - создание "замороженного" (неизменяемого) набора из перечисленных объектов.

* **globals()** - словарь с глобальными именами.

* **hasattr(object, name)** - проверка наличия атрибута у объекта.

* **hash(object)** - вычисление хэша.

* **help([object])** - встроенная помошь по объекту.

* **hex(x)** - шестнадцатиричное представление целого числа.

* **id(object)** - идентификатор (адрес) объекта. Два объекта с неперекрывающимися временами жизни могут иметь совпадающие идентификаторы (адреса).

* **input([prompt])** - ввод значения с консоли. Если загружен модуль `readline`, то функция ведет себя гораздо интеллектуальнее.





























