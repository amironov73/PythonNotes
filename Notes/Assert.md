### Инструкция assert

Пример `assert`:

```python
def apply_discount(product, discount):
    price = int(product['цена'] * (1.0 - discount))
    assert 0 <= price <= product['цена'], 'Неверная скидка!'
    return price
```

`assert` раскрывается примерно в следующее:

```python
if __debug__:
    if not выражение1:
        raise AssertionError(выражение2)
```
