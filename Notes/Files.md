### Работа с файлами

```python
with open("C:\\SomeFile.txt", 'r', encoding='cp1251') as f:
    for line in f:
        print(line, end='')
```


#### CSV-файлы

```python
import csv
with open('C:\\data.csv', 'r') as f:
    reader=csv.reader(f)
    for row in reader:
        print(row[0], ' - ', row[1], ' - ', row[2])
```