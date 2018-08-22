### Декораторы

```python
def decorator1(func):
    return lambda: func() + 1
 
def decorator2(func):
    def print_func():
        print(func())
    return print_func
 
@decorator2
@decorator1
def function():
    return 41
    
# по факту function = decorator2(decorator1(function))    
 
function()
# печатает "42" 
```

Еще пример:

```python
def make_bold(fn):
    def wrapped():
        return "<b>" + fn() + "</b>"
    return wrapped

def make_italic(fn):
    def wrapped():
        return "<i>" + fn() + "</i>"
    return wrapped

@make_bold
@make_italic
def hello():
    return "hello world"

print(hello()) 
# <b><i>hello world</i></b>
```

