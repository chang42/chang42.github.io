
# 容器(Containers)  
Python提供了许多种类型的容器(containers)，一些对象的序列可以被存储到容器内。Python容器的数据类型有：   
`list,
set,
dictionary,
OrderedDictionary
bytearray
array
string,
frozenset,
tuple,
bytes`

## 列表(lists)  
列表是一有序的序列，可以包含不同的对象类型。


```python
l = ['red', 'blue', 'green', 'black', 'white']
```


```python
type(l)
```




    list



### 列表索引  
列表通过索引来查看元素。  
#### 正向索引  
索引下标从0开始。


```python
l[2]
```




    'green'



#### 反向索引


```python
l[-1]
```




    'white'



### 切片  
切片的语法：  
`l[start:stop:stride]`  
索引下标i为：srart <= i < stop


```python
l
```




    ['red', 'blue', 'green', 'black', 'white']




```python
l[2:4]
```




    ['green', 'black']




```python
l[::2]
```




    ['red', 'green', 'white']



列表内的元素可以通过索引和切变修改：


```python
l[1] = 'yellow'
l
```




    ['red', 'yellow', 'green', 'black', 'white']




```python
l[2:4] = ['grey', 'purple']
l
```




    ['red', 'yellow', 'grey', 'purple', 'white']



列表内的元素可以为不同的类型：


```python
l = [3, -200, 'hello']
l
```




    [3, -200, 'hello']



### 列表操作  
添加和删除元素


```python
L = ['red', 'blue', 'green', 'black', 'white']
```


```python
L.append('pink')
L
```




    ['red', 'blue', 'green', 'black', 'white', 'pink']




```python
L.pop() #s删除并返回该元素
```




    'pink'




```python
L.extend(['pink', 'purple'])
L
```




    ['red', 'blue', 'green', 'black', 'white', 'pink', 'purple']




```python
L[:-2]
```




    ['red', 'blue', 'green', 'black', 'white']



反序


```python
L[::-1]
```




    ['purple', 'pink', 'white', 'black', 'green', 'blue', 'red']




```python
list(L)
```




    ['red', 'blue', 'green', 'black', 'white', 'pink', 'purple']




```python
L.reverse()
```


```python
L
```




    ['purple', 'pink', 'white', 'black', 'green', 'blue', 'red']



连接和重复


```python
L + L
```




    ['red',
     'blue',
     'green',
     'black',
     'white',
     'pink',
     'purple',
     'red',
     'blue',
     'green',
     'black',
     'white',
     'pink',
     'purple']




```python
L * 2
```




    ['red',
     'blue',
     'green',
     'black',
     'white',
     'pink',
     'purple',
     'red',
     'blue',
     'green',
     'black',
     'white',
     'pink',
     'purple']



排序


```python
sorted(L) #新对象
```




    ['black', 'blue', 'green', 'pink', 'purple', 'red', 'white']




```python
L.sort() #就地
L
```




    ['black', 'blue', 'green', 'pink', 'purple', 'red', 'white']




```python
dir(L)
```




    ['__add__',
     '__class__',
     '__contains__',
     '__delattr__',
     '__delitem__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__getitem__',
     '__gt__',
     '__hash__',
     '__iadd__',
     '__imul__',
     '__init__',
     '__init_subclass__',
     '__iter__',
     '__le__',
     '__len__',
     '__lt__',
     '__mul__',
     '__ne__',
     '__new__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__reversed__',
     '__rmul__',
     '__setattr__',
     '__setitem__',
     '__sizeof__',
     '__str__',
     '__subclasshook__',
     'append',
     'clear',
     'copy',
     'count',
     'extend',
     'index',
     'insert',
     'pop',
     'remove',
     'reverse',
     'sort']



## 字符串(Strings)  
### 生成字符串  
Python中使用单引号''或双引号""生成字符串。


```python
s = 'Hello world!'
s
```




    'Hello world!'




```python
s = "Hello world!"
s
```




    'Hello world!'



### 简单操作  
加法，字符串连接：


```python
s = 'Hello ' + 'world!'
s
```




    'Hello world!'



字符串与数字相乘，重复输出字符串：


```python
'hello'*3
```




    'hellohellohello'



字符串长度：


```python
len(s)
```




    12



索引字符串中的字符，或者一部分：


```python
s[1]
```




    'e'




```python
s[1:4]
```




    'ell'



成员运算符`in`和`not in`


```python
'H' in s
```




    True




```python
'M' in s
```




    False



原始字符串r/R


```python
print(r'\n')
```

    \n
    


```python
print(R'\n')
```

    \n
    

#### 转义字符  
|转义字符|描述|
|:-:|:-:|
|\(在行尾时)|续行符|
|\\|反斜杠符号|
|\'|单引号|
|\"|双引号|
|\a|响铃|
|\b|退格(Backspace)|
|\e|转义|
|\000|空|
|\n|换行|
|\v|纵向制表符|
|\t|横向制表符|
|\r|回车|
|\f|换页|
|\oyy|八进制数，yy代表的字符，例如：\o12代表换行|
|\xyy|十六进制数，yy代表的字符，例如：\x0a代表换行|
|\other|其它的字符以普通格式输出|

#### 字符串格式化  
字符串格式化符号  

|符号|描述|
|:-:|:-:|
|%c|格式化字符及其ASCII码|
|%s|格式化字符串|
|%d|格式化整数|
|%u|格式化无符号整数|
|%o|格式化无符号八进制数|
|%x|格式化无符号十六进制数|
|%X|格式化无符号十六进制数（大写）|
|%f|格式化浮点数字，可指定小数点后的精度|
|%e|用科学记数法格式化浮点数|
|%E|作用同%e，用科学记数法格式化浮点数|
|%g|%f和%e的简写|
|%G|%f和%E的简写|
|%p|用十六进制数格式化变量的地址|


```python
'An integer: %i ; a float: %f; another string: %s ' % (1, 0.1, 'string')
```




    'An integer: 1 ; a float: 0.100000; another string: string '



格式化操作符辅助指令：

|符号|功能|
|:-:|:-:|
|*|定义宽度或者小数点精度|
|-|用作左对齐|
|+|在正数前面显示加号（+）|
|`<sp>`|在正数面前显示空格|
|#|在在八进制数面前显示零（‘0’）,在十六进制前面显示‘0x’或者‘0X’|
|0|显示的数字前面填充‘0’而不是默认的空格|
|%|‘%%’输出一个单一的‘%’|
|(var)|映射变量（字典参数）|
|m.n.|m是显示的最小宽度，n是小数点后的位数（如果可用的话）|

#### 三引号  
python三引号允许一个字符串跨多行，字符串中可以包含换行符、制表符以及其他特殊字符。实例如下


```python
para_str = """这是一个多行字符串的实例
多行字符串可以使用制表符
TAB ( \t )。
也可以使用换行符 [ \n ]。
"""
print (para_str)
```

    这是一个多行字符串的实例
    多行字符串可以使用制表符
    TAB ( 	 )。
    也可以使用换行符 [ 
     ]。
    
    

#### 内建函数  
使用`dir()`来查看所有可以使用的方法：


```python
dir(s)
```




    ['__add__',
     '__class__',
     '__contains__',
     '__delattr__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__getitem__',
     '__getnewargs__',
     '__gt__',
     '__hash__',
     '__init__',
     '__init_subclass__',
     '__iter__',
     '__le__',
     '__len__',
     '__lt__',
     '__mod__',
     '__mul__',
     '__ne__',
     '__new__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__rmod__',
     '__rmul__',
     '__setattr__',
     '__sizeof__',
     '__str__',
     '__subclasshook__',
     'capitalize',
     'casefold',
     'center',
     'count',
     'encode',
     'endswith',
     'expandtabs',
     'find',
     'format',
     'format_map',
     'index',
     'isalnum',
     'isalpha',
     'isdecimal',
     'isdigit',
     'isidentifier',
     'islower',
     'isnumeric',
     'isprintable',
     'isspace',
     'istitle',
     'isupper',
     'join',
     'ljust',
     'lower',
     'lstrip',
     'maketrans',
     'partition',
     'replace',
     'rfind',
     'rindex',
     'rjust',
     'rpartition',
     'rsplit',
     'rstrip',
     'split',
     'splitlines',
     'startswith',
     'strip',
     'swapcase',
     'title',
     'translate',
     'upper',
     'zfill']



#### 使用`()`或者`\`来换行  
当代码太长或者为了美观起见时，可以使用两种方法来将一行代码转为多行代码：  
* ()  
* \


```python
a = ("hello, world! "
    "it's a nice day. "
    "my name is ...")
a
```




    "hello, world! it's a nice day. my name is ..."




```python
a = "hello, world! " \
    "it's a nice day. " \
    "my name is ..."
a
```




    "hello, world! it's a nice day. my name is ..."



#### 强制转换为字符串  
* `str(ob)`强制将`ob`转化为字符串。
* `repr(ob)`强制将`ob`转化成字符串。  


```python
str(0.1)
```




    '0.1'




```python
repr(0.1)
```




    '0.1'



#### 整数与不同进制的字符串的转化 


```python
hex(255)
```




    '0xff'




```python
oct(255)
```




    '0o377'




```python
bin(255)
```




    '0b11111111'




```python
int('23')
```




    23




```python
int('FF', 16)
```




    255




```python
int('377', 8)
```




    255




```python
int('11111111', 2)
```




    255




```python
float('3.5')
```




    3.5



## 字典  
字典为一键值对应的无序容器，键(keys)通过‘`:`’映射到键值(values)。

创建字典


```python
tel = dict(
    [('emmanuelle', 5752),
     ('sebastian', 5578)
    ])
```


```python
tel
```




    {'emmanuelle': 5752, 'sebastian': 5578}




```python
type(tel)
```




    dict




```python
tel = {'emmanuelle': 5752, 'sebastian': 5578}
```


```python
tel
```




    {'emmanuelle': 5752, 'sebastian': 5578}




```python
type(tel)
```




    dict



插入键值


```python
tel['francis'] = 5915
```


```python
tel
```




    {'emmanuelle': 5752, 'francis': 5915, 'sebastian': 5578}



查看键值


```python
tel['sebastian']
```




    5578



更新键值


```python
tel['sebastian'] = 2348
```


```python
tel
```




    {'emmanuelle': 5752, 'francis': 5915, 'sebastian': 2348}



字典中键必须为不可变的，值可以是任意对象。


```python
d = {'a':1, 'b':tel, 3:'hello'}
```


```python
d
```




    {'a': 1,
     'b': {'emmanuelle': 5752, 'francis': 5915, 'sebastian': 2348},
     3: 'hello'}



### 字典方法

#### `get`方法  
用索引可以找到一个键对应的值，但是当字典中没有这个键的时候，Python会报错，这时候可以使用字典的 get 方法来处理这种情况，其用法如下：
  
`d.get(key, default = None)`

返回字典中键 key 对应的值，如果没有这个键，返回 default 指定的值（默认是 None ）。


```python
tel = {'emmanuelle': 5752, 'sebastian': 5578}
```


```python
tel['alice']
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    <ipython-input-109-72a73042d2e9> in <module>()
    ----> 1 tel['alice']
    

    KeyError: 'alice'



```python
print(tel.get('alice'))
```

    None
    

#### pop 方法删除元素  

pop 方法可以用来弹出字典中某个键对应的值，同时也可以指定默认参数：  
  
`d.pop(key, default = None)`

删除并返回字典中键 key 对应的值，如果没有这个键，返回 default 指定的值（默认是 None ）。


```python
tel.pop('emmanuelle')
```




    5752




```python
tel
```




    {'sebastian': 5578}




```python
tel.pop('emmanuelle', 'none exist')
```




    'none exist'



#### in查询字典中是否有该键


```python
'emmanuelle' in tel
```




    False



#### keys 方法，values 方法和items 方法


```python
tel.keys()
```




    dict_keys(['sebastian'])




```python
tel.values()
```




    dict_values([5578])




```python
tel.items()
```




    dict_items([('sebastian', 5578)])



## 元组(Tuples)  
元组为不可变的有序序列，元组的的元素写在 `()` 之间，或者可以直接用 `,` 间隔。

生成元组


```python
t = (12345, 54321, 'hello!')
```


```python
type(t)
```




    tuple




```python
t
```




    (12345, 54321, 'hello!')




```python
t = 12345, 54321, 'hello!'
```


```python
type(t)
```




    tuple




```python
t
```




    (12345, 54321, 'hello!')



索引和切片


```python
t[0]
```




    12345




```python
t[0:2]
```




    (12345, 54321)



元组方法


```python
dir(t)
```




    ['__add__',
     '__class__',
     '__contains__',
     '__delattr__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__getitem__',
     '__getnewargs__',
     '__gt__',
     '__hash__',
     '__init__',
     '__init_subclass__',
     '__iter__',
     '__le__',
     '__len__',
     '__lt__',
     '__mul__',
     '__ne__',
     '__new__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__rmul__',
     '__setattr__',
     '__sizeof__',
     '__str__',
     '__subclasshook__',
     'count',
     'index']



旧式字符串格式化中参数要用元组；
在字典中当作键值；
数据库的返回值……

## 集合(Sets)  
无序，元素不重复。

生成集合


```python
s = set(('a', 'b', 'c', 'a'))
s
```




    {'a', 'b', 'c'}




```python
type(s)
```




    set




```python
s = set(['a', 'b', 'c', 'a'])
s
```




    {'a', 'b', 'c'}




```python
type(s)
```




    set




```python
s = {'a', 'b', 'c'}
s
```




    {'a', 'b', 'c'}




```python
type(s)
```




    set



创建空集合的时候只能用`set`来创建，因为在Python中`{}`创建的是一个空字典。

### 集合操作


```python
a = {1, 2, 3, 4}
b = {3, 4, 5, 6}
```

#### 并  


```python
a.union(b)
```




    {1, 2, 3, 4, 5, 6}




```python
b.union(a)
```




    {1, 2, 3, 4, 5, 6}




```python
a | b
```




    {1, 2, 3, 4, 5, 6}



#### 交


```python
a.intersection(b)
```




    {3, 4}




```python
b.intersection(a)
```




    {3, 4}




```python
a & b
```




    {3, 4}



#### 差


```python
a.difference(b)
```




    {1, 2}




```python
a - b
```




    {1, 2}




```python
b.difference(a)
```




    {5, 6}




```python
b - a
```




    {5, 6}



#### 对称差


```python
a.symmetric_difference(b)
```




    {1, 2, 5, 6}




```python
b.symmetric_difference(a)
```




    {1, 2, 5, 6}




```python
a ^ b
```




    {1, 2, 5, 6}



#### 包含关系


```python
a = {1, 2, 3}
b = {1, 2}
```


```python
b.issubset(a)
```




    True




```python
b <= a
```




    True




```python
a.issuperset(b)
```




    True




```python
a >= b
```




    True



判断是否真子集


```python
a < a
```




    False



### 集合方法


```python
dir(a)
```




    ['__and__',
     '__class__',
     '__contains__',
     '__delattr__',
     '__dir__',
     '__doc__',
     '__eq__',
     '__format__',
     '__ge__',
     '__getattribute__',
     '__gt__',
     '__hash__',
     '__iand__',
     '__init__',
     '__init_subclass__',
     '__ior__',
     '__isub__',
     '__iter__',
     '__ixor__',
     '__le__',
     '__len__',
     '__lt__',
     '__ne__',
     '__new__',
     '__or__',
     '__rand__',
     '__reduce__',
     '__reduce_ex__',
     '__repr__',
     '__ror__',
     '__rsub__',
     '__rxor__',
     '__setattr__',
     '__sizeof__',
     '__str__',
     '__sub__',
     '__subclasshook__',
     '__xor__',
     'add',
     'clear',
     'copy',
     'difference',
     'difference_update',
     'discard',
     'intersection',
     'intersection_update',
     'isdisjoint',
     'issubset',
     'issuperset',
     'pop',
     'remove',
     'symmetric_difference',
     'symmetric_difference_update',
     'union',
     'update']



向集合中添加单个元素


```python
s = {1, 2 ,3}
s.add(5)
s
```




    {1, 2, 3, 5}



向集合中添加多个元素


```python
s.update([5, 6, 7])
s
```




    {1, 2, 3, 5, 6, 7}



删除单个元素  
`remove`，元素在集合中不存在时会报错。  
`discard`，元素在集合中不存在时不会报错。


```python
s.remove(7)
s
```




    {1, 2, 3, 5, 6}




```python
s.remove(7)
```


    ---------------------------------------------------------------------------

    KeyError                                  Traceback (most recent call last)

    <ipython-input-177-ddb2923ada10> in <module>()
    ----> 1 s.remove(7)
    

    KeyError: 7



```python
s.discard(6)
s
```




    {1, 2, 3, 5}




```python
s.discard(6)
```

弹出元素


```python
s.pop()
```




    1




```python
s
```




    {2, 3, 5, 6}



从a中除去所有属于b的元素


```python
a = {1, 2, 3}
b = {4}
s = a.difference_update(b)
print(s)
```

## 赋值操作  

### 赋值机制  
* `x = 1` 

为变量值分配内存空间，然后让变量x指向该内存空间。


```python
x = 500
```

* y = x  
  
变量y指向同一内存空间。


```python
y = x
```


```python
id(x)
```




    140027209410928




```python
id(y)
```




    140027209410928



改变变量y指向的内存空间。


```python
y = 'foo'
```


```python
id(y)
```




    140027303764800



### 垃圾回收机制  
* `x = [500, 501, 502]`  
Python为三个PyInt分配内存空间`pos1`, `pos2`, `pos3`，然后为列表分配一段内存`pos4`，它包含三个位置，分别指向这三个内存空间，最后再让变量`x`指向这个列表。

|内存|命名空间|
|:-:|:-:|
|pos1:PyInt(500)(inmutable)|x:pos4|
|pos2:PyInt(501)(inmutable)||
|pos3:PyInt(502)(inmutable)||
|pos4:PyList(pos1, pos2, pos3)(mutable)||


```python
x = [500, 501, 502]
print(id(x[0]))
print(id(x[1]))
print(id(x[2]))
print(id(x))
```

    140027209410928
    140027147408432
    140027147408688
    140027209719432
    

* y = x  
将变量`y`指向`pos4`。

|内存|命名空间|
|:-:|:-:|
|pos1:PyInt(500)(inmutable)|x:pos4|
|pos2:PyInt(501)(inmutable)|y:pos4|
|pos3:PyInt(502)(inmutable)||
|pos4:PyList(pos1, pos2, pos3)(mutable)||


```python
y = x
print(id(x))
print(id(y))
```

    140027209719432
    140027209719432
    

* y[1] = 600  
首先为600分配内存空间`pos5`，再把`y[1]`的位置指向`pos5`。此时`pos2`的对象已经没有用了，Python会自动调用垃圾回收机制将它回收，释放其所占内存。  

|内存|命名空间|
|:-:|:-:|
|pos1:PyInt(500)(inmutable)|x:pos4|
|pos2:(Garbage Collection)|y:pos4|
|pos3:PyInt(502)(inmutable)||
|pos4:PyList(pos1, pos2, pos3)(mutable)||
|pos5:PyInt(600)(inmutable)||


```python
y[1] = 600
print(id(x[1]))
print(id(y[1]))
```

    140027209409584
    140027209409584
    

* y = [700, 800]  
首先创建这个列表，然后将变量`y`指向它。  

|内存|命名空间|
|:-:|:-:|
|pos1:PyInt(500)(inmutable)|x:pos4|
|pos3:PyInt(502)(inmutable)||
|pos4:PyList(pos1, pos2, pos3)(mutable)||
|pos5:PyInt(600)(inmutable)||
|pos6:PyInt(700)(inmutable)|y:pos8|
|pos7:PyInt(800)(inmutable)||
|pos8:PyList(pos6, pos7)(mutable)||


```python
y = [700, 800]
print(id(y))
print(id(x))
```

    140027207208200
    140027209719432
    
