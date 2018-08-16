### Модуль subprocess

Модуль `subprocess` позволяет запускать дочерние процессы и подключаться к их потокам ввода-вывода.

Простейший пример:

```python
import subprocess

subprocess.call('notepad.exe')
# 0
```

Обратите внимание, что `call` ждет завершения процесса и лишь после этого возвращает управление.

Можно передать аргументы:

```python
import subprocess

subprocess.call(['ping', 'google.com'])
```

#### Класс Popen

Класс `Popen` не ждет завершения дочернего процесса (если не попросить):

```python
import subprocess

process = subprocess.Popen(['notepad.exe', r'C:\Temp\file.txt'])
code = process.wait()
print(code)
```

Как связаться с запущенным процессом и получить его вывод:

```python
import subprocess

process = subprocess.Popen(['ping', 'google.com'], stdout=subprocess.PIPE)
data = process.communicate()  # дожидается завершения процесса 
print (data)
```

Перенаправить вывод можно:

* subprocess.PIPE
* subprocess.DEVNULL
* subprocess.STDOUT (для stderr)

#### Метод run

**run(args, \*, stdin=None, input=None, stdout=None, stderr=None, shell=False, cwd=None, timeout=None, check=False, encoding=None, errors=None, env=None)**

Возвращает объект типа `CompletedProcess`, у которого есть поля и методы:

* args
* returncode
* stdout
* stderr
* check_returncode()

```python
import subprocess

process = subprocess.run(['ping', 'google.com'], stdout=subprocess.PIPE, encoding='cp8666')
print(process.stdout)
# Обмен пакетами с google.com [64.233.165.138] с 32 байтами данных:
# Ответ от 64.233.165.138: число байт=32 время=80мс TTL=45
# Ответ от 64.233.165.138: число байт=32 время=72мс TTL=45
# Ответ от 64.233.165.138: число байт=32 время=72мс TTL=45
# Ответ от 64.233.165.138: число байт=32 время=76мс TTL=45
#
# Статистика Ping для 64.233.165.138:
#    Пакетов: отправлено = 4, получено = 4, потеряно = 0
#    (0% потерь)
# Приблизительное время приема-передачи в мс:
#    Минимальное = 72мсек, Максимальное = 80 мсек, Среднее = 75 мсек
```

В версии для Windows есть структура `STARTUPINFO`, полностью аналогичная такой же из WIN32 API