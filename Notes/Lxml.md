### Модуль lxml

#### Формирование документа

```python
from lxml.etree import *

doc = Element('root')
doc.append(Element('child_1', number='1', text='Hello 1'))
doc.append(Element('child_2', number='2', text='Hello 2'))
print(tostring(doc, pretty_print=True).decode())
# <root>
#  <child_1 number="1" text="Hello 1"/>
#  <child_2 number="2" text="Hello 2"/>
# </root>
```

или так:

```python
from lxml.etree import *

doc = Element('root')
SubElement(doc, 'child_1', number='1', side='top').text = 'The text'
SubElement(doc, 'child_2', number='2', side='bottom').text = 'Other text'
print(tostring(doc, pretty_print=True).decode())
# <root>
#  <child_1 number="1" side="top">The text</child_1>
#  <child_2 number="2" side="bottom">Other text</child_2>
# </root>
```

#### Парсинг

```python
from lxml.etree import *

doc = XML('''<root>
  <child_1>First</child_1>
  <child_2>Second</child_2>
</root>
''')
print(doc.getchildren()[1].texxt)
# Second
```

или так:

```python
from lxml.etree import *

text = '<root><child/></root>'
doc = fromstring(text)
```

из файла:

```python
from lxml import etree
doc = etree.parse('content-sample.xml')
```

#### XPath

```python
from lxml.etree import *

root = XML("<root><a x='123'>aText<b/><c/><b/></a></root>")
print(root.find("b"))
# None
print(root.find("a").tag)
# a
print(root.find(".//b").tag)
# b
print([ b.tag for b in root.iterfind(".//b") ])
# ['b', 'b' ]
```

#### ElementTree

```python
from lxml.etree import *
root = XML("<root><a x='123'>aText<b/><c/><b/></a></root>")
tree = ElementTree(root)
for b in tree.iterfind('.//b'):
    print(tree.getelementpath(b))
# a/b[1]
# a/b[2]
```
