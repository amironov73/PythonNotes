### Работа с файлами

#### Обычные файлы

**open(file, mode='r', buffering=-1, encoding=None, errors=None, newline=None, closefd=True, opener=None)**

```python
with open("C:\\SomeFile.txt", 'r', encoding='cp1251') as f:
    for line in f:
        print(line, end='')
```

Режимы доступа:

| Обозначение | Смысл 
|-------------|-------
| r | Чтение из файла (по умолчанию)
| w | Запись в файл (существующий файл усекается)
| x | Запись в файл, эксклюзивный режим (ошибка, если файл уже существует)
| a | Запись в файл, добавление информации в конец файла
| b | Двоичный режим
| t | Текстовый режим
| + | Чтение и запись одновременно
| U | Режим универсальных концов строки (устаревший)


#### CSV-файлы

```python
import csv
with open('C:\\data.csv', 'r') as f:
    reader=csv.reader(f)
    for row in reader:
        print(row[0], ' - ', row[1], ' - ', row[2])
```