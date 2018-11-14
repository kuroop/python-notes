# 14-nov-2018

### 9 - sys.getsizeof for int, byteobject, string

```python
Python 3.6.6 (default, Sep 12 2018, 18:26:19) 
[GCC 8.0.1 20180414 (experimental) [trunk revision 259383]] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> sys.getsizeof(1)
28
>>> sys.getsizeof('1')
50
>>> sys.getsizeof("1")
50
>>> sys.getsizeof(b'1')
34
>>> 
```

### 8 - SQLAlchemy simple example

- Object mapping to database
```python
import os,sys
from sqlalchemy import Column, ForeignKey, Integer, String
from sqlalchemy.ext.declarative import declarative_base
from sqlalchemy.orm import relationship, sessionmaker
from sqlalchemy import create_engine

Base = declarative_base()


class Person(Base):

    __tablename__ = 'person'

    person_id = Column(Integer, primary_key = True)
    person_name = Column(String(250), nullable = False)


class Address(Base):
    __tablename__ = 'address'
    
    id_ = Column(Integer, primary_key=True)
    street_name = Column(String(250))
    street_number = Column(String(250))
    post_code = Column(String(250), nullable=False)
    person_id = Column(Integer, ForeignKey('person.person_id'))
    person = relationship(Person)

engine = create_engine('sqlite:///sqlalchemy_example.db')

Base.metadata.create_all(engine)


Base.metadata.bind = engine

DBSession = sessionmaker(bind=engine)

session = DBSession()

new_person = Person(person_name='new person')
session.add(new_person)
session.commit()


new_address = Address(post_code='0001' , person=new_person)
session.add(new_address)
session.commit()


print(session.query(Person).all())


person = session.query(Person).first()
print(person.person_name)
```


### 7 - Pyglet multimedia library Hello World

```python
Python 3.6.6 (default, Sep 12 2018, 18:26:19) 
[GCC 8.0.1 20180414 (experimental) [trunk revision 259383]] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import pyglet
>>> window = pyglet.window.Window()
>>> label = pyglet.text.Label('Hello, world',
...                           font_name='Times New Roman',
...                           font_size=36,
...                           x=window.width//2, y=window.height//2,
...                           anchor_x='center', anchor_y='center')
>>> @window.event
... def on_draw():
...     window.clear()
...     label.draw()
... 
>>> pyglet.app.run()
```

### 6 - Sympy

```python
>>> from sympy import *
>>> x , y , z = symbols('x y z')
>>> x
x
>>> y
y
>>> z
z
>>> expr = cos(x) + 1
>>> expr.subs(x,y)
cos(y) + 1
>>> expr.subs(x, 0)
2
>>> expr.subs(y, 0)
cos(x) + 1
>>> expand_
expand_complex(      expand_log(          expand_multinomial(  expand_power_exp(    
expand_func(         expand_mul(          expand_power_base(   expand_trig(         
>>> expand_func((x+y)**2)
(x + y)**2
>>> expand_func((x+y)**2)
(x + y)**2
>>> symplify("(x+y)**2")
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
NameError: name 'symplify' is not defined
>>> sympify("(x+y)**2")
(x + y)**2
>>> 
```

### 5 - Newton Raphson

- https://en.wikipedia.org/wiki/Newton%27s_method

```python
H = 1e-5

def derivative(f,x): return (f(x+H) - f(x))/H
def newton(f, x): return x - ( f(x) / derivative(f,x))
def runner(f,n): 
    x = 0
    itr = 0
    while itr < n:
        x = newton(f,1) if itr == 0 else newton(f,x)
        itr = itr + 1
    return x

if __name__ == '__main__':
    import sys 
    print( runner( lambda x: eval(sys.argv[1]) , 100) )
```

```bash
python newton.py x*x-2
```


### 4 - Smallest Number in python

```python
Python 3.6.6 (default, Sep 12 2018, 18:26:19) 
[GCC 8.0.1 20180414 (experimental) [trunk revision 259383]] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import sys
>>> sys.float_info
sys.float_info(max=1.7976931348623157e+308, max_exp=1024, max_10_exp=308, min=2.2250738585072014e-308, min_exp=-1021, min_10_exp=-307, dig=15, mant_dig=53, epsilon=2.220446049250313e-16, radix=2, rounds=1)
>>> 
```

### 3 - SHA256 for subsequent bytes

```python
>>> hashlib.sha256(b'1').hexdigest()
'6b86b273ff34fce19d6b804eff5a3f5747ada4eaa22f1d49c01e52ddb7875b4b'
>>> hashlib.sha256(b'2').hexdigest()
'd4735e3a265e16eee03f59718b9b5d03019c07d8b6c51f90da3a666eec13ab35'
>>> hashlib.sha256(b'3').hexdigest()
'4e07408562bedb8b60ce05c1decfe3ad16b72230967de01f640b7e4729b49fce'
```

### 2 - Dunder import 

```python
Python 3.6.6 (default, Sep 12 2018, 18:26:19) 
[GCC 8.0.1 20180414 (experimental) [trunk revision 259383]] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> __import__('IPython').embed()
Python 3.6.6 (default, Sep 12 2018, 18:26:19) 
Type 'copyright', 'credits' or 'license' for more information
IPython 7.1.1 -- An enhanced Interactive Python. Type '?' for help.

In [1]: ls                                                                                                                                            
Desktop/	 Downloads/   Music/	  Public/	 Documents/	 Pictures/   __pycache__/	 

In [2]: #in IPython shell                                                                                                                             
```

### 1 - Floating point errors!

```python
Python 3.6.6 (default, Sep 12 2018, 18:26:19) 
[GCC 8.0.1 20180414 (experimental) [trunk revision 259383]] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> [0.1] * 10
[0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1, 0.1]
>>> sum( [0.1]*10)
0.9999999999999999
>>> import math
>>> math.fsum([0.1]*10)
1.0
>>> 
```