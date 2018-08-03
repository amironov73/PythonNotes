### Функции

#### Объявление

##### Параметры по умолчанию

```python
def say_hello(name, message='Hello'):
    print(message, name)
```

**Значения по умолчанию для аргументов вычисляются только один раз!** Решение проблемы: не используйте изменяемые объекты в качестве значений по умолчанию.

##### Вложенные функции:
```python
def outer():
    def inner():
        print('Inner')

    print('Outer')
    inner()
    print('Outer again')
    
outer()
# Outer
# Inner
# Outer again    
```

##### Неопределенное число параметров

Неименованных

```python
def say_hello(message, *names):
    for name in names:
        print(message, name)
        
say_hello('Hello', 'Tom', 'Tim', 'Ted')
```

Именованных

```python
def do_something(command, **kwargs):
    if 'delay' in kwargs:
        waitfor(kwargs['delay'])
        
def waitfor(period):
    pass        
```

#### Вызов

Список в качестве аргументов:

```python
args = [5,2]
pow(*args)
# возвращает pow(5,2), т. е. 25
```

Множество именованных аргументов:

```python
def do_something(command, **kwargs):
    pass

kwargs = {'actually_do_something': True, 'print_a_bunch_of_numbers': True}
do_something('print', **kwargs)
```

Запуск одной из нескольких функций при помощи словаря:

```python
def key_1_pressed():
    pass
    
def key_2_pressed():
    pass
    
def key_3_pressed():
    pass
    
def unknown_key_pressed():
    pass    
    
keycode = 2
functions = {1: key_1_pressed, 2: key_2_pressed, 3: key_3_pressed}
functions.get(keycode, unknown_key_pressed)()
```

Передача self вручную:

```python
class Class:
    def a_method(self):
        print('Привет, метод!')
 
instance = Class()
 
instance.a_method()
# печатает 'Привет, метод!'
 
Class.a_method(instance)
# печатает 'Привет, метод!' 
```

#### Проверка на существование метода или свойства

```python
class Class:
    answer = 42
 
hasattr(Class, 'answer')
# возвращает True
hasattr(Class, 'question')
# возвращает False 
getattr(Class, 'answer')
# возвращает 42
getattr(Class, 'question', 'Сколько будет 6x9?')
# возвращает "Сколько будет 6x9?"
getattr(Class, 'question')
# бросает исключение AttributeError 
```

#### Добавление метода после создания класса

```python
class Class:
   def method(self):
        print('Привет, Хабр')
 
instance = Class()
instance.method()
# печатает "Привет, Хабр"
 
def new_method(self):
    print('Хабр еще торт!')
 
Class.method = new_method
instance.method()
# печатает "Хабр еще торт!"
```