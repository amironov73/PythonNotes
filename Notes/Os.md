### Модуль os

* **name** - какой из модулей загружен в качестве реализации `os`: 'posix', 'nt' или 'java'.

* **environ** - словарь переменных окружения, **getenv(key, default=None)** - получение значения переменной, **putenv(key, value)** - установка значения переменной.

* **chdir(path)**, **getcwd()** - манипуляции с текущей директорией.

* **get_exec_path()** - получение PATH в виде списка.

* **getlogin()** - логин текущего пользователя.

* **getpid()** - идентификатор текущего процесса.

* **strerror(code)** - получение формулировки ошибки, проще говоря, "что не так".

#### Операции с файлами и директориями

* **fdopen(fd, *args, **kwargs)** - открытие файла по его дескриптору.

* **close(fd)** - закрытие.

* **dup(fd)** - создание дубликата.

* **fsync(fd)** - сброс кэша для даного файла на диск. Аналогично **sync()**

* **lseek(fd, pos, how)** - позиционирование по файлу.

* **open(path, flags, mode=0o777, \*, dir_fd=None)** - открытие файла. Режимы: O_RDONLY, O_WRONLY, O_RDWR, O_APPEND, O_CREAT, O_EXCL, O_TRUNC. Только в Windows доступны: O_BINARY, O_NOINHERIT, O_SHORT_LIVED, O_TEMPORARY, O_RANDOM, O_SEQUENTIAL, O_TEXT. 

* **pipe()** - создание канала.
 
* **read(fd, n)** - чтение из файла. **write(fd, str)** - запись.
 
* **truncate(path, length)** - изменение длины файла.
 
* **get_terminal_size(fd=STDOUT_FILENO)** - получение размера консоли (терминала).
 
* **terminal_size** - размер консоли (терминала).
 
* **chdir(path)** - смена текущей папки. **getcwd()** - получение текущей папки.
 
* **listdir(path='.')** - считывание папки.
 
* **mkdir(path, mode=0o777, \*, dir_fd=None)** - создание папки.
 
* **remove(path, \*, dir_fd=None)** - удаление файла.
 
* **removedirs(name)** - рекурсивное удаление папки.
 
* **rename(src, dst, \*, src_dir_fd=None, dst_dir_fd=None)** - переименование файла.
 
* **rmdir(path, \*, dir_fd=None)** - нерекурсивное удаление папки.
 
* **scandir(path='.')** - возвращает итератор, считывающий файлы и подпапки. По окончании необходимо вызвать `scandir.close()`. Итератор выдает объекты типа DirEntry. У каждого из них есть поля `name`, `path`, методы `is_dir()`, `is_file()`, `is_symlink()` и `stat()`.
 
* **walk(top, topdown=True, onerror=None, followlinks=False)** - обход файловой системы (генератор).
 
#### Процессы

* **abort()** - посылает SIGABRT текущему процессу.

* **execl(path, arg0, arg1, ...)**, **execle(path, arg0, arg1, ..., env)**, 
**execlp(file, arg0, arg1, ...)**, **execlpe(file, arg0, arg1, ..., env)**, 
**execv(path, args)**, **execve(path, args, env)**, **execvp(file, args)**, 
**execvpe(file, args, env)** - запуск дочернего процесса.

* **_exit(n)** - немедленное завершение текущего процесса без вызова обрабочтиков.

* **system(command)** - запуск системного шелла с указанной командой.

#### Прочее

* **cpu_count()** - количество процессоров. Может вернуть `None`.

* **sep** - разделитель элементов пути.

* **linesep** - разделитель строк: '\n' или '\r\n'.


 
 
 
 
 
 
 






