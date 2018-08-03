### Функции-генераторы

```python
import random

def random_numbers(high=1000):
    while True:
        yield random.randint(0, high)
```