### Правдивость объектов

Следующие объекты выдают `False`:

* None
* '' (пустая строка)
* 0 (целый 0)
* 0.0 (плавающий 0)
* [] (пустой список)
* вообще все пустые контейнеры: списки, кортежи, словари, множества. 


Класс может сам определятьс свою правдивость:

```python
class MyClass:
    
    def __init__(self, n: int):
        self.n = n

    def __bool__(self):
        return self.n > 0
        
        
c = MyClass(1)
if c:
    print('n > 0')
else:
    print('n <= 0')        
```