### Модуль threading

```python
import threading
import time
 
class MyThread(threading.Thread):
    def run(self):
        print('Start', self.getName())
        time.sleep(1)
        print('Finish', self.getName())

for x in range(4):
    my_thread = MyThread(name='Thread-{}'.format(x + 1))
    my_thread.start()
    time.sleep(0.9)
```

Результат:

```text
Start Thread-1
Start Thread-2
Finish Thread-1
Start Thread-3
Finish Thread-2
Start Thread-4
Finish Thread-3
Finish Thread-4
```

* **active_count()** - число живых объектов `Thread` в данный момент.

* **current_thread()** - текущий объект `Thread`. Может быть возвращен dummy-объект, если текущий поток создан не с помощью модуля `threading`.

* **get_ident()** - идентификатор текущего потока (целое число).

* **enumerate()** - перечисление активных объектов `Thread`.

* **main_thread()** - главный объект `Thread`.

#### Объекты Thread

Конструктор: **threading.Thread(group=None, target=None, name=None, args=(), kwargs={}, *, daemon=None)**. Здесь `target` - то, что будет вызвано методом `run()`, а `args` - аргументы, которые будут переданы в вызываемый метод.

* **start()** - запуск потока

* **run()** - полезная нагрузка потока

* **join(timeout=None)** - ожидание завершения

* **name** - имя

* **ident** - идентификатор

* **is_alive()** - жив ли поток

#### Объекты Lock

* **acquire(blocking=True, timeout=-1)** - захват блокировки

* **release()** - освобождение

Есть ещё объекты RLock, которые отличаются тем, что их можно безопасно многократно захватывать из одного потока.

Как лучше захватывать:

```python
import threading

some_lock = threading.Lock()
with some_lock:
    # do something
    pass
```

