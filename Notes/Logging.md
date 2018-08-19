### Модуль logging

Модуль предоставляет привычные методы `debug()`, `info()`, `warning()`, `error()` и `critical()`.

#### Уровни логирования

| Уровень | Для чего предназначен
|---------|----------------------
| DEBUG | Используется при отладке, для выяснения, как, например, менялись значения переменных по ходу дела
| INFO | Подтверждение того, что все работает, как задумано
| WARNING | Предупреждение о том, что произошло то, чего не ожидали или о возможных будущих проблемах ("мало свободного места на диске")
| ERROR | Серьезная проблема, мешающая выполнять некоторые функции ("нет прав на запись в папку")
| CRITICAL | Серьещная проблема, не дающая продолжать работу программы ("невозможно открыть файл конфигурации")

#### Настройка формата сообщений

```python
import logging

logging.basicConfig(format='%(levelname)s:%(message)s', 
                    level=logging.DEBUG)
```

Сообщения будут выглядеть так:

```text
DEBUG:This message should appear on the console
INFO:So should this
WARNING:And this, too
```

Можно добавить дату/время:

```python
import logging

logging.basicConfig(format='%(asctime)s %(message)s')
logging.warning('is when this event was logged.')
```

Результат:

```text
2010-12-12 11:41:42,612 is when this event was logged.
```

#### Примеры

Вывод предупреждения

```python
import logging

logging.warning('Не стой под грузом и стрелой!')
```

Логирование в файл

```python
import logging

logging.basicConfig(filename='example.log', level=logging.DEBUG)
logging.debug('Приложение успешно запущено')
```