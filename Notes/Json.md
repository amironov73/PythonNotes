### Модуль json

#### Сериализация

Со встроенными типами все просто:

```python
import json
json.dumps(['foo', {'bar': ('baz', None, 1.0, 2)}])
# '["foo", {"bar": ["baz", null, 1.0, 2]}]'
```

Можно немного ужаться за счет пробелов:

```python
import json
json.dumps([1, 2, 3, {'4': 5, '6': 7}], separators=(',', ':'))
# '[1,2,3,{"4":5,"6":7}]'
```

Можно наоборот, сделать красиво:

```python
import json
print(json.dumps({'4': 5, '6': 7}, sort_keys=True, indent=4))
# {
#    "4": 5,
#    "6": 7
# }
```

#### Десериализация

```python
import json
json.loads('["foo", {"bar":["baz", null, 1.0, 2]}]')
# ['foo', {'bar': ['baz', None, 1.0, 2]}]
```

#### Encoder

Сложные типы требуют энкодера:

```python
import json
class ComplexEncoder(json.JSONEncoder):
     def default(self, obj):
         if isinstance(obj, complex):
             return [obj.real, obj.imag]
         # Let the base class default method raise the TypeError
         return json.JSONEncoder.default(self, obj)

json.dumps(2 + 1j, cls=ComplexEncoder)
# '[2.0, 1.0]'
ComplexEncoder().encode(2 + 1j)
# '[2.0, 1.0]'
list(ComplexEncoder().iterencode(2 + 1j))
# ['[2.0', ', 1.0', ']']
```

Во многих случаях можно обойтись простейшим энкодером, который выдает `__dict__`

```python
import json

class Person:
	def __init__(self,name,age):
		self.name = name
		self.age = age
		
class SimpleEncoder(json.JSONEncoder):
	def default(self, o):
		return o.__dict__
		
person = Person('Alexey', 44)
json.dumps(person, cls=SimpleEncoder)
# '{"name": "Alexey", "age": 44}'				
```

Десериализация заключается в обратном трюке с `__dict__`

```python
import json

class Person:
    def __init__(self):
        self.name = ''
        self.age = 0
        
    def __str__(self):
        return self.name + ' is ' + str(self.age) + ' years old'
        
    @staticmethod
    def deserialize(s):
        result = Person()
        result.__dict__ = json.loads(s)
        return result
        
person = Person.deserialize('{"name": "Alexey", "age": 44}')
print(person)
# Alexey is 44 years old        
```

#### Методы

* **dump(obj, fp, \*, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, default=None, sort_keys=False, \*\*kw)** - вывод в поток `fp`.

* **dumps(obj, \*, skipkeys=False, ensure_ascii=True, check_circular=True, allow_nan=True, cls=None, indent=None, separators=None, default=None, sort_keys=False, \*\*kw)** - выдача строки с JSON.

* **load(fp, \*, cls=None, object_hook=None, parse_float=None, parse_int=None, parse_constant=None, object_pairs_hook=None, \*\*kw)** - загрузка объекта из файла `fp`.

* **loads(s, \*, encoding=None, cls=None, object_hook=None, parse_float=None, parse_int=None, parse_constant=None, object_pairs_hook=None, \*\*kw)** - загрузка объекта из строки.

 

 
