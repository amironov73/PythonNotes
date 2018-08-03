### Исключения

Перехват и обработка:

```python
try:
    a = 1
    b = 0
    c = a / b
except:
    print('Что-то пошло не так')
finally:
    print('Будет выполнено в любом случае')    
```

Расширенный вариант:

```python
try:
    a = input('Введите что-нибудь')
    b = int(a)
    print(b)
    c = 1 / b
except ValueError as e:
    print('Ошибка преобразования')
    print('Аргументы исключения:', e.args)
except ZeroDivisionError:
    print('Деление на ноль')
except Exception:
    print('Не знаю что, но что-то пошло не так')
finally:
    print('Будет выполнено в любом случае')            
```

Возбуждение исключения:

```python
a = int(input('На что будем делить?'))
if a == 0:
    raise ZeroDivisionError('На ноль делить нельзя!')
```