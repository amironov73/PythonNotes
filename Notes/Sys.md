### Модуль sys

* **argv** - аргументы командной строки, в т. ч. `argv[0]` - имя скрипта (если скрипт введен с клавиатуры или задан в командной строке интерпретатора, то пусто).

* **byteorder** - порядок байт на машине. `'big'` означает Big Endian, `'little'` привычный нам интеловский.

* **builtin_module_names** - имена модулей, вкомпилированных в интерпретатор. В моем случае

```
('_ast', '_bisect', '_blake2', '_codecs', '_codecs_cn', '_codecs_hk',
 '_codecs_iso2022', '_codecs_jp', '_codecs_kr', '_codecs_tw', '_collections',
 '_csv', '_datetime', '_functools', '_heapq', '_imp', '_io', '_json',
 '_locale', '_lsprof', '_md5', '_multibytecodec', '_opcode', '_operator',
 '_pickle', '_random', '_sha1', '_sha256', '_sha3', '_sha512', '_signal',
 '_sre', '_stat', '_string', '_struct', '_symtable', '_thread', '_tracemalloc',
 '_warnings', '_weakref', '_winapi', 'array', 'atexit', 'audioop', 'binascii',
 'builtins', 'cmath', 'errno', 'faulthandler', 'gc', 'itertools', 'marshal',
 'math', 'mmap', 'msvcrt', 'nt', 'parser', 'sys', 'time', 'winreg',
 'xxsubtype', 'zipimport', 'zlib')
```

* **call_tracing(func, args)** - установка перехватчика вызовов функций.

* **dont_write_bytecode** - говорит интерпретатору, что не нужно сохранять на диск .pyc.

* **excepthook(type, value, traceback)** - вызывается при возникновении неперехваченного исключения. Предполагается, что должна вывести информацию об этом исключении на экран.

* **exc_info()** - информация об обрабатываемом в настоящее время исключении.

* **executable** - полный путь к исполняемому файлу интерпретатора (там, где это имеет смысл).

* **exit([arg])** - выход из интерпретатора. Реализовано как возбуждение исключения SystemExit.

* **flags** - флаги командной строки (debug, inspect, interactive, dont_write_bytecode, no_user_site, no_site, ignore_environment, verbose, quiet, hash_randomization).

* **getdefaultencoding()** получение кодировки по умолчанию.

* **getfilesystemencoding()** - получение кодировки файловой системы.

* **getrefcount(object)** - число ссылок на данный объект.

* **getsizeof(object[, default])** - размер данного объекта (очень неточно!).

* **gettrace()** - получение трассирующей функции, установленной с помощью settrace().

* **getwindowsversion()** - версия Windows.

* **implementation** - информация о реализации Python. В моем случае

```
namespace(cache_tag='cpython-36', hexversion=50726384, name='cpython',
 version=sys.version_info(major=3, minor=6, micro=5, releaselevel='final',
 serial=0))
```

* **int_info** - информация об используемом представлении целых чисел. В моем случае

```
sys.int_info(bits_per_digit=30, sizeof_digit=4)
```

* **is_finalizing()** - возвращает `True`, если интерпретатор завершает работу.

* **maxunicode** - наибольший возможный на данный момент Unicode code point. Равен 1114111 (т. е. 0x10FFFF).

* **modules** - словарь со всеми загружеными в настоящий момент модулями.

* **path** - пути, по которым интерпретатор ищет модули при импорте. В моем случае

```
['', 'C:\\Python36-x64\\Lib\\idlelib', 'C:\\Python36-x64\\python36.zip',
 'C:\\Python36-x64\\DLLs', 'C:\\Python36-x64\\lib', 'C:\\Python36-x64',
 'C:\\Python36-x64\\lib\\site-packages']
```

* **path_hooks** - список методов, вызываемых при поиске модулей. В моем случае

```
[<class 'zipimport.zipimporter'>, <function FileFinder.path_hook.<locals>
.path_hook_for_FileFinder at 0x00000193BBDEC6A8>]
```

* **platform** - идентификатор платформы: 'linux', 'win32', 'cygwin' или 'darwin'.

* **stdin**, **stdout** и **stderr** - стандартные потоки ввода-вывода.

* **`__stdin__`**, **`__stdout__`** и **`__stderr__`** - стандартные потоки, созданные при старте интерпретатора (чтобы можно было вернуть обратно)/

* **version** - версия интерпретатора в виде строки. В моем случае

```
'3.6.5 (v3.6.5:f59c0932b4, Mar 28 2018, 17:00:18) [MSC v.1900 64 bit (AMD64)]'
```