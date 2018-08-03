### Пользовательский интерфейс на Tk

Простейшая программа

```python
from tkinter import *
 
root = Tk()
root.title("Графическая программа на Python")
root.geometry("400x300")
 
root.mainloop()
```

Привязка действий:

```python
from tkinter import *
 
clicks = 0

def click_button():
    global clicks
    clicks += 1
    root.title("Clicks {}".format(clicks))
 
root = Tk()
root.title("GUI на Python")
root.geometry("300x250")
 
btn = Button(text="Click Me", background="#555", foreground="#ccc",
             padx="20", pady="8", font="16", command=click_button)
btn.pack()
 
root.mainloop()
```

Изменение текста на кнопке:

```python
from tkinter import *
 
clicks = 0
 
def click_button():
    global clicks
    clicks += 1
    buttonText.set("Clicks {}".format(clicks))
 
root = Tk()
root.title("GUI на Python")
root.geometry("300x250")
 
buttonText = StringVar()
buttonText.set("Clicks {}".format(clicks))
 
btn = Button(textvariable=buttonText, background="#555", foreground="#ccc",
             padx="20", pady="8", font="16", command=click_button)
btn.pack()
 
root.mainloop()
```

Аналогично имеются: IntVar, BooleanVar, DoubleVar

Можно использовать метод `config`:

```python
from tkinter import *
 
clicks = 0
 
def click_button():
    global clicks
    clicks += 1
    btn.config(text="Clicks {}".format(clicks))
 
root = Tk()
root.title("GUI на Python")
root.geometry("300x250")
 
btn = Button(text="Click Me", padx="20", pady="8", font="16")
btn.config(command=click_button)
btn.pack()
 
root.mainloop()
```