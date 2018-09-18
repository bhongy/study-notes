## String

```python
# repeat a string
'abc' * 3 # -> 'abcabcabc'

# best way to format a string
f = 'foo'
b = 'bar'
foobar = '{foo}{bar}'.format(foo=f, bar=b)

# formatting float precision points in string
'number: {num:.3f}'.format(num=3.14159265359)

# python3.6+ f-string instead of .format()
num = 3.14159265359
f'number: {num:.3f}'
```

## List

```python
# delete (mutate) a range of items from a list
del my_list[1:5]

# list comprehension
# [<expression> for <var> in <source_list>]
# [<expression> for <x> in <xs> for <y> in <ys>]
# [<expression> for <var> in <source_list> if <conditional>]
pow2 = [2 ** x for x in range(10)]
```

## Sets

```python
# casting from list to set
set([1,1,1,1,2,2,3]) # -> {1,2,3}
```

## Files

```python
f = open('/path/to/file.txt')
content = f.read()
f.seek(0) # reset read cursor
f.close() # important! must close the file after open

# alternative, don't need to manually .close()
with open('/path/to/file.txt') as f:
    content = f.read()

# mode='r', read only
# mode='w', write only (overwrite existing or create new)
# mode='a', append only
# mode='r+', read and write
# mode='w+', read and write (create new if not existed)
# mode='w+', read and write (create new if not existed)
with open('file.txt', mode='w') as f:
    f.write('the quick brown fox')
```

## Loop

```python
# destructuring tuple
my_list = [(1,2), (3,4), (5,6)]
for a, b in my_list:
    # ...

my_dict = { 'k1': 1, 'k2': 2 }
for key in my_dict:
    # ...
for key, value in my_dict.items():
    # ...

word = 'abcd' # or a list
for index, value in enumerate(word):
    # ...

# does list contains (also works with string)
'x' in ['x', 'y', 'z'] # -> True

# dictionary contains key
'foo' in { 'foo': 'bar' } # -> True

# dictionary contains value
'bar' in { 'foo': 'bar' }.values() # -> True
```

## Operators

```python
from random import randint
i = randint(0, 100)
```

## OOP

```python
class MyClass():
    # class attribute
    some_attribute = 42 # same for all 

    def __init__(self, foo):
        # instance attribute
        self.foo = foo

my_instance = MyClass('bar')
# keyword argument also works
my_instance = MyClass(foo='bar')

print my_instance.some_attribute 
# alternative way to access class attribute
print MyClass.some_attribute # Better
print my_instance.foo
```

## Modules & Packages

Create `__init__.py` in a folder to create a package.

```python
# from <Package (folder)> import <Module (file)>
# import <Module>
# from Foo.Bar import Baz
```