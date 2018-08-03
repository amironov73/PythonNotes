### Кодировки

Супер-метод шифрования `rot13`:

```text
>>> 'Hello world!'.encode('rot13')
'Uryyb jbeyq!'
>>> 'Uryyb jbeyq!'.decode('rot13')
u'Hello world!'
```

Экранирование символов в строке:
```text
>>> s = 'Hello\\n\\rworld!'
>>> s
'Hello\\n\\rworld!'
>>> repr(s)
"'Hello\\\\n\\\\rworld!'"
>>> print s.decode('string_escape')
Hello
world!
```