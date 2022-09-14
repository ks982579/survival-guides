# Python OS module

## Miscellaneous Operating System Interfaces

[python_docs/os](https://docs.python.org/3/library/os.html)
[MarkDown](https://www.markdownguide.org/)

>Provides a portable way of using operating system dependent functionality.

__Note__: All functions in this module raise ```OSError``` in the case of errors. 

```Python
import os
os.error
```
> An alias for the built-in ```OSError``` exception.
---
```python
os.name
```
> The name of the OS dependent module improted. 
---
### __File Names, CMD Line Arguments, and Env Vars__
Python UTF-8 Mode ignores the locale encoding and forces the usage ofthe UTF-8 encoding. The standard stream setting in UTF-8 mode can be overridden by ```PYTHONIOENCODING```. 

As a result, command line arguments, environment variables and fileneames are decoded to text using the UTF-8 encoding. 

```python
os.ctermid()
```
> Return the filename corresponding to the controlling terminal of the process. 
---
```python
import os
env_map = os.environ
print(env_map['ENV_NAME'])
```
A [mapping](https://docs.python.org/3/glossary.html#term-mapping) object where keys and values are strings that represent the process environment. 

Methods inherited from ```collections.abc.MutableMapping```
```python
clear(self) -> None # Removes all iteams.
pop(self, key, default=<object object at 0x000001D390248160>) -> v # Remove and return (key, value) tuple; or raise KeyError.
popitem(self) -> (k,v) # Remove and return some (key, value) tuple.
update(self, other=(), /, **kwargs) -> None # 
```
Methods inherited from ```collections.abc.Mapping```
```python
get(self, key, default=None)
items(self)
keys(self)
values(self)
```
---
