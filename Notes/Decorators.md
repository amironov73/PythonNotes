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

