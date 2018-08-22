### Символ подчеркивания

См. заметку https://hackernoon.com/understanding-the-underscore-of-python-309d1a029edc

Символ подчеркивания в Python трактуется специальным образом.

Во-первых, _ понимается как "тут должна быть переменная, но она мне не нужна":

```python
for _ in range(10):
    print('Something')
```

или так:

```python
x, _, y = (1, 2, 3)
# x = 1, y = 3
```

В Python 3 также доступна расширенная распаковка кортежей:

```python
x, *_, y = (1, 2, 3, 4, 5)
# x = 1, y = 5
```

Во-вторых, в интерпретаторе _ означает результат последнего вычисления:

```text
>>> 2 + 3
5
>>> _ * 2
10
```

В-третьих, имена, начинающиеся с подчеркивания, считаются приватными в классах и модулях. Такие имена не импортируются с помощью `from module import *`. 

Конечно же, ничего по-настоящему приватного в Python нет и быть не может, это просто соглашение: "не вызывайте эту функцию, она для внутреннего употребления". Если очень хочется, всегда можно заимпортировать внутреннюю функцию и вызвать ее:

```text
from module import _internal_function

_internal_function('Ha-ha!')
```

В-четвертых, имена, оканчивающиеся подчеркиванием, применяются, чтобы избежать конфликта с зарезервированными словами:

```text
Tkinter.Toplevel(master, class_='ClassName') # Avoid conflict with 'class' keyword

list_ = List.objects.get(1) # Avoid conflict with 'list' built-in type
```

Имена атрибутов, начинающиеся с двух подчеркиваний, искажаются специальным образом, чтобы сделать их принадлежащими данному конкретному классу. Python добавляет к ним `_ClassName` спереди:

```python
class A:
    def __double_method(self):  # станет _A__double_method
        pass
        
class B(A):
    def __double_method(self):  # станет _B__double_method
        pass        
```

В-пятых, имена, начинающиеся и заканчивающиеся двойным подчеркиванием, считаются "магическими" и зарезервированы для Python (например, `__len__`, `__init__`). Не следует самому давать такие имена атрибутам.

В-шестых, подчеркивание активно используется при локализации программ, например, с помощью модуля `gettext`:

```python
import gettext

gettext.bindtextdomain('myapplication', '/path/to/my/language/files')
gettext.textdomain('myapplication')
_ = gettext.gettext
print (_('This is translatable string.'))
```

В-седьмых, начиная с Python 3.6, стало возможно разделять группы цифр в числовых литералах с помощью подчеркивания:

```python
dec_base = 1_000_000
bin_base = 0b_1111_0000
hex_base = 0x_1234_ABCD
```