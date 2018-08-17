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

* **int(x,base=10)** - преобразование в целое.

* **isinstance(object, classinfo)** - является ли данный объект экземпляром указанного класса (или его потомка).

* **issubclass(class, classinfo)** - является ли данный класс потомком (подклассом) указанного класса.

* **iter(object\[,sentinel\])** = запрос итератора у объекта.

* **len(s)** - запрос длины у объекта. Контейнеры возвращают количество элементов в них, прочие объекты могут сами определить метод `__len__`.

* **list(\[iterable\])** - построение списка из последовательности.

* **locals()** - словарь локальных имен. Обратите внимание, имя может одновременно входить и в `locals()` и в `globals()`.

* **map(function, iterable)** - отображение последовательности с помощью указанного метода.

```python
x = [-1, 2, -3]
y = list(map(abs, x))
```

* **max(iterable, \*\[, key, default\])** - поиск максимального элемента в последовательности.

* **memoryview(obj)** - доступ к памяти объекта.

* **min(iterabke, \*\[, key, default\])** - поиск минимального элемента в последовательности.

* **next(iterator\[, default\])** - продвижение итератора. По достижении конца последовательности либо возвращается `default` (если задано), либо выбрасывается исключение `StopIteration`.

* **oct(x)** - восмиричное представление числа.

* **open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)** - открытие файла.

* **ord(c)** - порядковый номер символа.

* **pow(x, y\[, z\])** - возведение в степень. z = модуль, по которому необходимо выполнить деление: `pow(x,y) % z`.

* **print(\*objects, sep=' ', end='\\n', file=sys.stdout, flush=False)** - вывод в файл (по умолчанию в стандартный выходной поток).

* **property(fget=None, fset=None, fdel=None, doc=None)** - регистрация свойства объекта:

```python
class C:
    def __init__(self):
        self._x = None

    def getx(self):
        return self._x

    def setx(self, value):
        self._x = value

    def delx(self):
        del self._x

    x = property(getx, setx, delx, "I'm the 'x' property.")
```

Можно организовать то же самое с помощью декоратора:

```python
class Parrot:
    def __init__(self):
        self._voltage = 100000

    @property
    def voltage(self):
        """Get the current voltage."""
        return self._voltage
```

* **range(start, stop\[, step\])** или просто **range(stop)** - последовательность чисел.

* **repr(object)** - строковое представление объекта. Предполагается, что возвращенное значение можно передать `eval` и получить такой же объект.

* **reversed(seq)** - обращение последовательности.

* **round(number\[, ndigits\])** - округление числа.

* **set(\[iterable\])** - множество из последовательности.

* **setattr(object, name, value)** - установка значения атрибута.

* **slice(start, stop\[, step\])** или просто **slice(stop)** - получение среза списка (не копирование!).

* **sorted(iterable, \*, key=None, reverse=False)** - сортировка последовательности.

* **@staticmethod** - объявление метода статическим, т. е. не требующим `self`.

* **class str(object=b'', encoding='utf-8', errors='strict')** - получение строкового представления объекта.

* **sum(iterable\[, start\])** - суммирование последовательности.

* **super(\[type\[, object-or-type\]\])** - получение прокси-объекта, который перенаправляет вызовы методов в класс-предок (суперкласс).

* **tuple(\[iterable\])** - создание кортежа из последовательности.

* **type(object)** или **type(name, bases, dict)** - получение типа объекта.

* **vars(\[object\])** - получение словаря `__dict__` для модуля, класса, экземпляра или любого другого объекта, имеющего атрибут `__dict__`.

* **zip(\*iterables)** - сшивание двух и более последовательностей.

* **\_\_import\_\_(name, globals=None, locals=None, fromlist=(), level=0)** - эта функция вызывается оператором `import`.

 

























