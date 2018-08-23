### Магические методы

Статья https://habr.com/post/186608/

Магические методы позволяют задать поведение экземпляров ваших классов в определенных ситуациях.

#### Конструирование и удаление объектов

* **\_\_init\_\_ (self, ...)** - наверное, самый известный магический метод. Он вызывается при создании экземпляра объекта.

* **\_\_new\_\_ (cls, ...)** - предшественник `__new__`. Именно он конструирует новый экземпляр объекта, который затем в виде `self` попадает в `__init__`. Обратите внимание, это метод класса, а не экземпляра! С помощью `__new__` можно возвращать уже существующий экземпляр вместо создания нового (получится синглтон)!

* **\_\_del\_\_ (self)** - деструктор, ответственный за уничтожение экземпляра объекта.

Пример совместной работы `__init__` и `__del__`:

```python
from os.path import join

class FileObject:

    def __init__(self, filepath='~', filename='sample.txt'):
        self.file = open(join(filepath, filename), 'r+')

    def __del__(self):
        self.file.close()
        del self.file
```

#### Сравнение объектов

* **\_\_cmp\_\_ (self, other)** - самый базовый из методов сравнения. **В Python 3 больше нет!**

* **\_\_eq\_\_ (self, other)** - оператор `==`.

* **\_\_ne\_\_ (self, other)** - оператор `!=`.

* **\_\_lt\_\_ (self, other)** - оператор `<`.

* **\_\_gt\_\_ (self, other)** - оператор `>`.

* **\_\_le\_\_ (self, other)** - оператор `<=`.

* **\_\_ge\_\_ (self, other)** - оператор `>=`.

```python
class Word(str):
    """Класс для слов, определяющий сравнение по длине слов."""

    def __new__(cls, word):
        # Мы должны использовать __new__, так как тип str неизменяемый
        # и мы должны инициализировать его раньше (при создании)
        if ' ' in word:
            print("Value contains spaces. Truncating to first space.")
            word = word[:word.index(' ')] # Теперь Word это все символы до первого пробела
        return str.__new__(cls, word)

    def __gt__(self, other):
        return len(self) > len(other)
    def __lt__(self, other):
        return len(self) < len(other)
    def __ge__(self, other):
        return len(self) >= len(other)
    def __le__(self, other):
        return len(self) <= len(other)
```

#### Числовые магические методы

Унарные операторы

* **\_\_pos\_\_ (self)** - унарный плюс `+some_object`.

* **\_\_neg\_\_ (self)** - отрицание `-some_object`.

* **\_\_abs\_\_ (self)** - для функции `abs()`.

* **\_\_invert\_\_ (self)** - инвертирование `~`.

* **\_\_round\_\_ (self)** - для функции `round()`.

* **\_\_floor\_\_ (self)** - для функции `math.floor()`.

* **\_\_ceil\_\_ (self)** - для функции `math.ceil()`.

* **\_\_trunc\_\_ (self)** - для функции `math.trunc()`.

Обычные арифметические операторы

* **\_\_add\_\_ (self, other)** - сложение `a + b`.

* **\_\_sub\_\_ (self, other)** - вычитание `a - b`.

* **\_\_mul\_\_ (self, other)** - умножение `a * b`.

* **\_\_floordiv\_\_ (self, other)** - целочисленное деление `a // b`.

* **\_\_div\_\_ (self, other)** - деление `a / b`. **В Python 3 больше нет, т. к. деление по умолчанию правильное (см. ниже)!**

* **\_\_truediv\_\_ (self, other)** - правильное деление. Работает после `from __future__ import division`.

* **\_\_mod\_\_ (self, other)** - деление по модулю `a % b`.

* **\_\_divmod\_\_ (self, other)** - для функции `divmod()`.

* **\_\_pow\_\_ (self, other)** - возведение в степень `a ** b`.

* **\_\_lshift\_\_ (self, other)** - сдвиг влево `a << b`.

* **\_\_rshift\_\_ (self, other)** - сдвиг вправо `a >> b`.

* **\_\_and\_\_ (self, other)** - двоичное И `a & b`.

* **\_\_or\_\_ (self, other)** - двоичное ИЛИ `a | b`.

* **\_\_xor\_\_ (self, other)** - исключающее ИЛИ `a ^ b`.

Отраженные операторы

* **\_\_radd\_\_ (self, other)** - отраженное сложение.

* **\_\_rsub\_\_ (self, other)** - отраженное вычитание.

* **\_\_rmul\_\_ (self, other)** - отраженное умножение.

* **\_\_rfloordiv\_\_ (self, other)** - отраженное целочисленное деление.

* **\_\_rdiv\_\_ (self, other)** - отраженное деление.

* **\_\_rtruediv\_\_ (self, other)** - отраженное правильное деление.

* **\_\_rmod\_\_ (self, other)** - отраженное деление по модулю.

* **\_\_rdivmod\_\_ (self, other)** - для отраженной функции `divmod()`.

* **\_\_rpow\_\_ (self, other)** - отраженное возведение в степень.

* **\_\_rlshift\_\_ (self, other)** - отраженный сдвиг влево.

* **\_\_rrshift\_\_ (self, other)** - отраженный сдвиг вправо.

* **\_\_rand\_\_ (self, other)** - отраженное двоичное И.

* **\_\_ror\_\_ (self, other)** - отраженное двоичное ИЛИ.

* **\_\_rxor\_\_ (self, other)** - отраженное исключающее ИЛИ.

Составное присваивание

* **\_\_iadd (self, other)\_\_** - сложение с присваиванием `a += b`.

* **\_\_isub (self, other)\_\_** - вычитание с присваиванием `a -= b`.

* **\_\_imul (self, other)\_\_** - умножение с присваиванием `a *= b`.

* **\_\_ifloordiv (self, other)\_\_** - целочисленное деление с присваиванием `a //= b`.

* **\_\_idiv (self, other)\_\_** - деление с присваиванием `a += b`.

* **\_\_itruediv (self, other)\_\_** - правильное деление с присваиванием `a /= b`.

* **\_\_imod (self, other)\_\_** - деление по модулю с присваиванием `a ^= b`.

* **\_\_ipow (self, other)\_\_** - возведение в степень с присваиванием `a **= b`.

* **\_\_ilshift (self, other)\_\_** - сдвиг влево с присваиванием `a <<= b`.

* **\_\_irshift (self, other)\_\_** - сдвиг вправо с присваиванием `a >>= b`.

* **\_\_iand (self, other)\_\_** - логическое И с присваиванием `a &= b`.

* **\_\_ior (self, other)\_\_** - логическое ИЛИ с присваиванием `a |= b`.

* **\_\_ixor (self, other)\_\_** - исключающее ИЛИ с присваиванием `a ^= b`.

#### Преобразование типов

* **\_\_int(self)\_\_** - преобразование в `int`.

* **\_\_long(self)\_\_** - преобразование в `long`.

* **\_\_float(self)\_\_** - преобразование в `float`.

* **\_\_complex(self)\_\_** - преобразование в `complex`.

* **\_\_oct(self)\_\_** - преобразование в восмеричное число.

* **\_\_hex(self)\_\_** - преобразование в шестнадцатиричное число.

* **\_\_index(self)\_\_** - преобразование в `int`, когда объект используется в срезах `[start:stop:step]`.

* **\_\_trunc(self)\_\_** - для функции `math.trunc()`.

* **\_\_coerce(self)\_\_** - метод для реализации арифметики с операндами разных типов. `__coerce__` должен вернуть None если преобразование типов невозможно. Если преобразование возможно, он должен вернуть пару (кортеж из 2-х элементов) из `self` и `other`, преобразованных к одному типу. **В Python 3 больше нет!**

#### Строковое представление

* **\_\_str\_\_(self)** - для функции `str()`.

* **\_\_repr\_\_(self)** - для функции `repr()`. Желательно возвращать валидный код на Python.

* **\_\_unicode\_\_(self)** - для функции `unicode()`. **В Python 3 больше нет! (зато см. ниже)**

* **\_\_bytes(self)\_\_** - В Python 3 выдает представление в однобайтовой кодировке.

* **\_\_format\_\_(self, formatstr)** - для функции `format()`

#### Прочее

* **\_\_hash\_\_(self)** - для функции `hash()`.

* **\_\_bool\_\_(self)** - для функции `bool()`.

* **\_\_dir\_\_(self)** - для функции `dir()`. Может потребоваться для интерактивных сценариев.

* **\_\_sizeof\_\_(self)** - для функции `sys.getsizeof()`.

* **\_\_getattr\_\_(self, name)** - вызывается, когда пытаются получить значение НЕСУЩЕСТВУЮЩЕГО атрибута.

* **\_\_getattribute\_\_(self, name)** - вызывается, когда пытаются получить значение ЛЮБОГО атрибута.

```python
def __getattribute__(self, name):
    return  self.__dict__[name]  # Как-то так
```

* **\_\_setattr\_\_(self, name, value)** - вызывается при любой попытке установки значения ЛЮБОГО атрибута.

```python
def __setattr__(self, name, value):
    self.__dict__[name] = value  # Как-то так
```

* **\_\_delattr\_\_(self, name)** - вызывается при попытке удалить ЛЮБОЙ атрибут.

```python
def __delattr__(self, name):
    self.__dict__.remove(name)
```

Пример подсчета обращений к атрибутам:

```python
class AccessCounter(object):
    """Класс, содержащий атрибут value и реализующий счётчик доступа к нему.
    Счётчик увеличивается каждый раз, когда меняется value."""

    def __init__(self, val):
        super(AccessCounter, self).__setattr__('counter', 0)
        super(AccessCounter, self).__setattr__('value', val)

    def __setattr__(self, name, value):
        if name == 'value':
            super(AccessCounter, self).__setattr__('counter', self.counter + 1)
        # Не будем делать здесь никаких условий.
        # Если вы хотите предотвратить изменение других атрибутов,
        # выбросьте исключение AttributeError(name)
        super(AccessCounter, self).__setattr__(name, value)

    def __delattr__(self, name):
        if name == 'value':
            super(AccessCounter, self).__setattr__('counter', self.counter + 1)
        super(AccessCounter, self).__delattr__(name)
```

#### Контейнеры

* **\_\_len\_\_(self)** - для функции `len()`.

* **\_\_getitem\_\_(self, key)** - для получения элемента через `self[key]`.

* **\_\_setitem\_\_(self, key, value)** - для установки значения элемента через `self[key] = value`.

* **\_\_iter\_\_(self)** - вызывается функцией `iter()`. Возвращает итератор для контейнера.

* **\_\_next\_\_(self)** - вызывается функцией `next()`. Метод должен либо вернуть следующее значение из последовательности, либо выбросить `StopIteration`.

* **\_\_reversed\_\_(self)** - для функции `reversed()`.

* **\_\_contains\_\_(self, item)** - для оператора `in`.

* **\_\_missing\_\_(self, key)** - используется при наследовании от `dict`. Определяет поведение для для каждого случая, когда пытаются получить элемент по несуществующему ключу.

Пример:

```python
class FunctionalList:
    """Класс-обёртка над списком с добавлением некоторой функциональной магии: head,
    tail, init, last, drop, take."""

    def __init__(self, values=None):
        if values is None:
            self.values = []
        else:
            self.values = values

    def __len__(self):
        return len(self.values)

    def __getitem__(self, key):
        # если значение или тип ключа некорректны, list выбросит исключение
        return self.values[key]

    def __setitem__(self, key, value):
        self.values[key] = value

    def __delitem__(self, key):
        del self.values[key]

    def __iter__(self):
        return iter(self.values)

    def __reversed__(self):
        return FunctionalList(reversed(self.values))

    def append(self, value):
        self.values.append(value)
        
    def head(self):
        # получить первый элемент
        return self.values[0]
        
    def tail(self):
        """получить все элементы после первого"""
        return self.values[1:]
        
    def init(self):
        """получить все элементы кроме последнего"""
        return self.values[:-1]
        
    def last(self):
        """получить последний элемент"""
        return self.values[-1]
        
    def drop(self, n):
        """все элементы кроме первых n"""
        return self.values[n:]
        
    def take(self, n):
        """первые n элементов"""
        return self.values[:n]
```

#### Рефлексия

* **\_\_instancecheck\_\_(self, instance)** - для функции `isinstance(instance, class)`. Проверяет, является ли экземпляр членом нашего класса.

* **\_\_subclasscheck\_\_(self, subclass)** - для функции `issubclass(subclass, classs)`. Проверяет, наследуется ли класс от нашего.

#### Вызываемые объекты (callable)

* **\_\_call\_\_(self, args)** - позволяет экземпляру класса быть вызванным так, будто он функция.

Пример

```python
class Entity:

	def __init__(self):
		self.x = 0
		self.y = 0
		
	def __call__(self, x, y):
		self.x = x
		self.y = y
		
	def __str__(self):
		return f'x={self.x}; y={self.y}'

e = Entity()
e(1, 2)
print(e)
# x=1; y=2
```

#### Менеджеры контекста

* **\_\_enter\_\_(self)** - вход в блок. Возвращаемое значение и есть то, с чем производятся операции внутри `with`.

* **\_\_exit\_\_(self, exception_type, exception_value, traceback)** - определяет действия менеджера контекста после того, как блок будет выполнен (или прерван во время работы). Может использоваться для контроля исключений, чистки, любых действий которые должны быть выполнены незамедлительно после блока внутри with. Если блок выполнен успешно, exception_type, exception_value, и traceback будут установлены в None. В другом случае вы сами выбираете, перехватывать ли исключение или предоставить это пользователю; если вы решили перехватить исключение, убедитесь, что `__exit__` возвращает `True` после того как всё сказано и сделано. Если вы не хотите, чтобы исключение было перехвачено менеджером контекста, просто позвольте ему случиться.

Пример

```python
class Closer:
    """Менеджер контекста для автоматического закрытия объекта вызовом метода close 
    в with-выражении."""

    def __init__(self, obj):
        self.obj = obj

    def __enter__(self):
        return self.obj # привязка к активному объекту with-блока

    def __exit__(self, exception_type, exception_val, trace):
        try:
           self.obj.close()
        except AttributeError: # у объекта нет метода close
           print('Not closable.')
           return True # исключение перехвачено
```

#### Дескрипторы

Дескрипторы это такие классы, с помощью которых можно добавить свою логику к событиям доступа (получение, изменение, удаление) к атрибутам других объектов. Дескрипторы не подразумевается использовать сами по себе; скорее, предполагается, что ими будут владеть какие-нибудь связанные с ними классы.

* **\_\_get\_\_(self, instance, owner)** - определяет поведение при возвращении значения из дескриптора. `instance` это объект, для чьего атрибута-дескриптора вызывается метод. `owner` это тип (класс) объекта.

* **\_\_set\_\_(self, instance, value)** - определяет поведение при изменении значения из дескриптора. `instance` это объект, для чьего атрибута-дескриптора вызывается метод. `value` это значение для установки в дескриптор.

* **\_\_delete\_\_(self, instance)** - определяет поведение для удаления значения из дескриптора. `instance` это объект, владеющий дескриптором.


Пример: преобразование единиц измерения

```python
class Meter(object):
    """Дескриптор для метра."""

    def __init__(self, value=0.0):
        self.value = float(value)
        
    def __get__(self, instance, owner):
        return self.value
        
    def __set__(self, instance, value):
        self.value = float(value)


class Foot(object):
    """Дескриптор для фута."""

    def __get__(self, instance, owner):
        return instance.meter * 3.2808
        
    def __set__(self, instance, value):
        instance.meter = float(value) / 3.2808


class Distance(object):
    """Класс, описывающий расстояние, содержит два дескриптора для футов и
    метров."""
    meter = Meter()
    foot = Foot()    
```

#### Клонирование объектов

* **\_\_copy\_\_(self)** - для функции `copy.copy()`.

* **\_\_deepcopy\_\_(self, memodict={})** - для функции `copy.deepcopy()`. `memodict` - это кэш предыдущих скопированных объектов, он предназначен для оптимизации копирования и предотвращения бесконечной рекурсии, когда копируются рекурсивные структуры данных. Когда вы хотите полностью скопировать какой-нибудь конкретный атрибут, вызовите на нём copy.deepcopy() с первым параметром memodict.