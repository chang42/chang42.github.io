
# 脚本和模块（scripts and modules）  

## 脚本  
Python文件的扩展名为`.py`，首先我们来写一个Python脚本：


```python
%%writefile test.py

words = 'It is a Python script.'

def sentencesplit(sentence):
    for word in sentence.split():
        print(word)
    return

sentencesplit(words)
```

    Writing test.py
    

执行：


```python
%run test.py
```

    It
    is
    a
    Python
    script.
    

同时，脚本中的变量和函数也被载入当前环境：


```python
words
```




    'It is a Python script.'




```python
sentencesplit(words)
```

    It
    is
    a
    Python
    script.
    

Python脚本可以当作模块，通过 `import` 关键词加载执行：


```python
import test
```

    It
    is
    a
    Python
    script.
    


```python
test
```




    <module 'test' from '/home/chang/notebooks/Learning Python/test.py'>



同时脚本 `test.py` 中的变量和函数都被载入了当前环境，通过  
```
module.var/foo
```
查看变量或调用函数：


```python
test.words
```




    'It is a Python script.'




```python
test.sentencesplit("It's a Python script.")
```

    It's
    a
    Python
    script.
    

## 从对象中导入模块

导入模块


```python
import os
```


```python
os
```




    <module 'os' from '/home/chang/miniconda3/lib/python3.6/os.py'>



删除文件：


```python
import os
os.remove('test.py')
```


```python
from os import remove
remove('test.py')
```


```python
from os import *
remove('test.py')
```

## 创建模块  
在大型工程中，如果希望定义的对象（变量、函数、类）重复使用，可以通过创建自定义模块来实现。


```python
%%writefile demo.py

"""A demo module."""

def print_a():
    """Prints a."""
    print('a')
    
def print_b():
    """Prints b."""
    print('b')
    
c = 2
d = 2
```

    Writing demo.py
    

在文件中，定义了函数 `print_a` 和 `print_b` 。如果我们在编译器内想调用函数 `print_a` ，可以将执行该脚本，或者将其作为模块引入：  
```
import module
module.object
```


```python
import demo
```


```python
demo.print_a()
```

    a
    


```python
demo.print_b()
```

    b
    


```python
demo?
```


```python
who
```

    demo	 
    


```python
whos
```

    Variable   Type      Data/Info
    ------------------------------
    demo       module    <module 'demo' from '/hom<...>Learning Python/demo.py'>
    


```python
dir(demo)
```




    ['__builtins__',
     '__cached__',
     '__doc__',
     '__file__',
     '__loader__',
     '__name__',
     '__package__',
     '__spec__',
     'c',
     'd',
     'print_a',
     'print_b']




```python
from demo import print_a, print_b
```


```python
whos
```

    Variable   Type        Data/Info
    --------------------------------
    demo       module      <module 'demo' from '/hom<...>Learning Python/demo.py'>
    print_a    function    <function print_a at 0x7fb878178bf8>
    print_b    function    <function print_b at 0x7fb878178b70>
    

重新载入模块


```python
import importlib
importlib.reload(demo)
```




    <module 'demo' from '/home/chang/notebooks/Learning Python/demo.py'>



## `__name__` 属性  
如果想将一个 `.py` 文件即当作脚本，又当做模块，可以使用 `__name__` 属性。  
只有当文件被当作脚本执行的时候， `__name__` 的值才会是 `__mian__` 


```python
%%writefile demo2.py

"""A demo module."""

def print_a():
    """Prints a."""
    print('a')
    
def print_b():
    """Prints b."""
    print('b')

# print_b() runs on import
print_b()

if __name__ == '__main__':
    # print_a() is only excuted when the module is run directly.
    print_a()
```

    Overwriting demo2.py
    


```python
import demo2
```


```python
%run demo2.py
```

    b
    a
    

![](__name__.jpg)

## 管理代码  
* 经常使用的指令集写进函数中，以增加代码可重复利用性。
* 经常调用的函数或者代码块写进模块中，以在不同的脚本中引用模块。

### 模块路径和导入  
`import modules` 会从默认路径中的文件中寻找该模块。通过 `sys.path` 查看默认路径。


```python
import sys
sys.path
```




    ['',
     '/home/chang/miniconda3/lib/python36.zip',
     '/home/chang/miniconda3/lib/python3.6',
     '/home/chang/miniconda3/lib/python3.6/lib-dynload',
     '/home/chang/miniconda3/lib/python3.6/site-packages',
     '/home/chang/miniconda3/lib/python3.6/site-packages/IPython/extensions',
     '/home/chang/.ipython']



自定义模块须位于该路径下的文件夹中，或者将自定义模块的位置添加到Python的默认路径中。可以通过注册表项修改或者利用 `sys.path` 模块，写一段Python脚本。


```python
import sys
new_path = '/home/chang/notebooks/user_defined_modules'
if new_path not in sys.path:
    sys.path.append(new_path)
```

## 包（Packages）  
包是指拥有许多模块的文件夹，其本身也是一个模块，拥有许多子模块，其中比较特殊的是 `__init__.py` ，它告诉Python该文件夹是Python包，可以从其里面导入模块。


```python
import scipy
```


```python
scipy.__file__
```




    '/home/chang/miniconda3/lib/python3.6/site-packages/scipy/__init__.py'




```python
import scipy.version
```


```python
scipy.version.version
```




    '0.19.1'


