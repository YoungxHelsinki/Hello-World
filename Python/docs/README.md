# Python main cheat sheet
## [Ternary Operators](http://book.pythontips.com/en/latest/ternary_operators.html)
```python
is_fat = True
state = "fat" if is_fat else "not fat"
```

## [set](http://book.pythontips.com/en/latest/ternary_operators.html)
```python
some_list = ['a', 'b', 'c', 'b', 'd', 'm', 'n', 'n']
duplicates = set([x for x in some_list if some_list.count(x) > 1])
print(duplicates)
# Output: set(['b', 'n'])

valid = set(['yellow', 'red', 'blue', 'green', 'black'])
input = set(['red', 'brown'])
print(input.intersection(valid))
# Output: set(['red'])
print(input.difference(valid))
# Output: set(['brown'])
```

## [Decorators](http://book.pythontips.com/en/latest/decorators.html)
```python
from datetime import datetime
from functools import wraps

def timed(func):
  ''' Benchmarking wrapper
  @wraps preserves the pre-decorated function's property.
  e.g., some_func.__name__ will return "some_func" not "decorated" '''
  @wraps(func)
  def decorated(*args, **kwargs):
    pre_t = datetime.utcnow()
    result = func(*args, **kwargs)
    post_t = datetime.utcnow()
    duration = (post_t - pre_t).total_seconds()
    print "\t%s: %.2f sec" % (func, duration)
    return result
  return decorated

@timed
def some_func():
  pass
```

## [Mutation](http://book.pythontips.com/en/latest/mutation.html)
Whenever you assign a variable to another variable of mutable datatype, any changes to the data are reflected by both variables. The new variable is just an alias for the old variable. This is only true for mutable datatypes
```python
def add_to(num, target=[]):
    target.append(num)
    return target

add_to(1)
# Output: [1]

add_to(2)
# Output: [1, 2]

add_to(3)
# Output: [1, 2, 3]
```
 In Python the default arguments are evaluated once when the function is defined, not each time the function is called. You should never define default arguments of mutable type unless you know what you are doing. You should do something like this:
```python
def add_to(element, target=None):
    if target is None:
        target = []
    target.append(element)
    return target

```

## [\__slots__](http://tech.oyster.com/save-ram-with-python-slots/)

By default Python uses a dict to store an object’s instance attributes. Which is usually fine, and it allows fully dynamic things like setting arbitrary new attributes at runtime.

However, for small classes that have a few fixed attributes known at “compile time”, the dict is a waste of RAM, and this makes a real difference when you’re creating a million of them. You can tell Python not to use a dict, and only allocate space for a fixed set of attributes, by settings \__slots__ on the class to a fixed list of attribute names:

```python
class Image(object):
    __slots__ = ['id', 'caption', 'url']

    def __init__(self, id, caption, url):
        self.id = id
        self.caption = caption
        self.url = url
        self._setup()

    # ... other methods ...
cat = Image(1, "cat", "path/to/cat")
cat.url = "new_path/to/cat"   # Works fine
cat.age = 1                   # Raise an AttributeError
cat.__dict__                  # Raise an AttributeError
```
**Warning:** Don’t prematurely optimize and use this everywhere! It’s not great for code maintenance, and it really only saves you when you have thousands of instances. This only runs on [new style classes](http://stackoverflow.com/a/54873/3067013).

**Tip:** [PyPy](http://pypy.org/) automatically does \__slots__ and other optimization



## [enumerate](http://book.pythontips.com/en/latest/enumerate.html)
```python
my_list = ['apple', 'banana', 'grapes', 'pear']
counter_list = list(enumerate(my_list, 1))
print(counter_list)
```

## Get Bluetooth Mac addresses
```python
import bluetooth
nearby_devices = bluetooth.discover_devices()
for mac_address in nearby_devices:
  print mac_address
```

## Write object to a file
```python
import pickle

with open(filename, 'wb') as f:
  pickle.dump(nearby_devices, f)

if os.path.isfile(filename):
  print "read list"
  with open(filename, 'rb') as f:
    existing_bt_list = pickle.load(f)
```

## Swap keys and values in a dict
```python
{v:k for k, v in dictionary.items()}
```

## Give parameter name for format strings
```python
colors = ['red', 'green', 'blue', 'yellow']
for index, color in enumerate(colors):
    print "{index} --> {color}".format(index=index, color=color)
```

## [Built-in function: iter(o[, sentinel])](https://docs.python.org/2/library/functions.html#iter)
Return an iterator object. The first argument is interpreted very differently depending on the presence of the second argument. Without a second argument, o must be a collection object which supports the iteration protocol (the __iter__() method), or it must support the sequence protocol (the __getitem__() method with integer arguments starting at 0). If it does not support either of those protocols, TypeError is raised. If the second argument, sentinel, is given, then o must be a callable object. The iterator created in this case will call o with no arguments for each call to its next() method; if the value returned is equal to sentinel, StopIteration will be raised, otherwise the value will be returned.<br>

One useful application of the second form of iter() is to read lines of a file until a certain line is reached. The following example reads a file until the readline() method returns an empty string:
```python
with open('mydata.txt') as fp:
    for line in iter(fp.readline, ''):
        process_line(line)
```

## [Distinguising multiple exit points in loops](https://youtu.be/OSGv2VnC0go?t=1058)
```python
def find(seq, tgt):
    for i, v in enumerate(seq):
        if v == tgt:
            break
    else:   # 'nobreak' would have been a better name than 'else'
        return False
    return i
```

## Reverse a string
```python
"Hello!"[::-1]
```

## example
```python
```

## example
```python
```
