
# THREADING in Python

* Creation
* Lock
* Async Write (Class Inherit)


```python
from threading import Thread
import time

def SayIt(name,repeat):
    delay = 0.2
    print(name + ' --- Started')
    for i in range(repeat):
        time.sleep(delay)
        print(name + "*" * (i+1))
    print(name + " --- Completed")
```


```python
SayIt("Alec",5)
SayIt("Jim",5)
```

>     Alec --- Started
>     Alec*
>     Alec**
>     Alec***
>     Alec****
>     Alec*****
>     Alec --- Completed
>     Jim --- Started
>     Jim*
>     Jim**
>     Jim***
>     Jim****
>     Jim*****
>     Jim --- Completed
>

```python
t1 = Thread(target=SayIt,args=("Alec",5))
t2 = Thread(target=SayIt,args=("Jim",5))
t1.start()
#t1.join()
t2.start()
t2.join()

```

>     Alec --- Started
>     Jim --- Started
>     Alec*
>     Jim*
>     Alec**
>     Jim**
>     Alec***
>     Jim***
>     Alec****
>     Jim****
>     Alec*****
>     Alec --- Completed
>     Jim*****
>     Jim --- Completed
>

```python
import threading 
import time

tLock = threading.Lock()

x = 0

def Add(repeat):
    global x
    #delay = 0.0001
    for i in range(repeat):
        tLock.acquire
        x = x + 1
        tLock.release

t1 = Thread(target=Add,args=(100000,))
t2 = Thread(target=Add,args=(100000,))
t1.start()
t2.start()

print(x)
```

>     138806
>


### THREADING - Games and Graphics
* Example using  **turtle**


```python
import turtle
import threading 

def draw_spiral(my_turtle,line_len):
    if line_len > 0:
        my_turtle.forward(line_len)
        my_turtle.right(90)
        draw_spiral(my_turtle, line_len - 5)

def draw_playground(myTurtle):
    myTurtle.color('red', 'blue')
    myTurtle.begin_fill()
    while True:
        myTurtle.forward(170)
        myTurtle.left(200)
        if abs(myTurtle.pos()) < 1:
            break
    myTurtle.end_fill()

def StartDrawing():
    spiral = turtle.Turtle()
    playground = turtle.Turtle()
    spiral.pu()
    spiral.setx(-300)
    spiral.pd()

    
      
    draw_spiral(spiral, 90)
    draw_playground(playground)
    
    
    turtle.Screen().exitonclick()

StartDrawing()
```


```python
import turtle
import threading 

def draw_spiral(my_turtle,line_len):
    if line_len > 0:
        my_turtle.forward(line_len)
        my_turtle.right(90)
        draw_spiral(my_turtle, line_len - 5)

def draw_playground(myTurtle):
    myTurtle.color('red', 'blue')
    myTurtle.begin_fill()
    while True:
        myTurtle.forward(170)
        myTurtle.left(200)
        if abs(myTurtle.pos()) < 1:
            break
    myTurtle.end_fill()

def StartDrawing():
    spiral = turtle.Turtle()
    playground = turtle.Turtle()
    spiral.pu()
    spiral.setx(-300)
    spiral.pd()

    
    
    spiral_thread = threading.Thread(target=lambda: draw_spiral(spiral, 90))
    playground_thread = threading.Thread(target=lambda: draw_playground(playground))
    spiral_thread.start()
    playground_thread.start()
    
    turtle.Screen().exitonclick()

StartDrawing()
```

## THREADING - WEB API

* Example: Stock Prices
* https://www.alphavantage.co/documentation/
* Get API KEY - https://www.alphavantage.co/support/#api-key


```python
import requests
from pprint import pprint
    
def getLastUpdated(symbol): 
    url = 'https://www.alphavantage.co/query?function=TIME_SERIES_DAILY&symbol=%s&apikey=*****************'
    data = requests.get(url % symbol).json()
    pprint(data)
    pprint(data['Meta Data']['3. Last Refreshed'])

getLastUpdated('AAAP') #'AAPL') #'MSFT') #
```


```python
url = 'https://www.alphavantage.co/query?function=TIME_SERIES_DAILY&symbol=%s&apikey=*******************'
data = requests.get(url % 'MSFT').json()
data
```


```python
last_day = list(data['Time Series (Daily)'])[0]
last_day
```


```python
data['Time Series (Daily)'][last_day]['1. open']
```


```python
import requests
import time
    
def getLastPrice(symbol):
    url = 'https://www.alphavantage.co/query?function=TIME_SERIES_DAILY&symbol=%s&apikey=***************'
    data = requests.get(url % symbol).json()
    out = symbol + ' -->  '
    try:
        last_day = list(data['Time Series (Daily)'])[0]
        out += data['Time Series (Daily)'][last_day]['1. open']
    except:
        pass
    print(out)
    
    


SYMBOLs = open(r'symbols.txt').read().split()
start = time.time()
for symbol in SYMBOLs[:50]:
    getLastPrice(symbol)

print("Job time:", time.time() - start)

```


```python
import csv
import requests
from threading import Thread
import threading
import time

def getLastPrice(symbol):
    url = 'https://www.alphavantage.co/query?function=TIME_SERIES_DAILY&symbol=%s&apikey=****************'
    data = requests.get(url % symbol).json()
     
    out = symbol + ' -->  '
    try:
        last_day = list(data['Time Series (Daily)'])[0]
        out += data['Time Series (Daily)'][last_day]['1. open']
    except:
        pass
    #tLock.acquire()
    print(out)
    #tLock.release()
        
threadlist = []
SYMBOLs = open(r'symbols.txt').read().split()

tLock = threading.Lock()

start = time.time()

for symbol in SYMBOLs[:50]:
    t = Thread(target=getLastPrice,args=(symbol,))
    t.start()
    threadlist.append(t)

for t in threadlist:
    t.join()

print("Job time:", time.time() -start)


```

## • Async Write (Class Inherit)


```python
import threading
import time

class AsyncWrite(threading.Thread):
    def __init__(self, text, out):
        threading.Thread.__init__(self)
        self.text = text
        self.out = out

    def run(self):
        f = open(self.out, "a")
        for i in range(100000):
            f.write(self.text + '\n')
        f.close()
        print("Finished Background file write to " + self.out)

if __name__ == '__main__':    
    
    start = time.time()
    backgrounds = []
    for i in range(10):
        message = 'Some text in file %d' % i 
        background = AsyncWrite(message, 'out%d.txt' % i)
        background.start()
        backgrounds.append(background)
    for i in range(10):
        backgrounds[i].join()
    
    print("Threading - Job time:", time.time() -start)
    '''
     
    start = time.time()
    for i in range(10):
        message = 'Some text in file %d' % i 
        out = 'sout%d.txt' % i
        f = open(out, "a")
        for i in range(100000):
            f.write(message + '\n')
        f.close()
        print("Finished file write to " + out)
    
    print("Seq - Job time:", time.time() -start)
    '''
```
