
# 文件读写（Input and Output）  
在文件中读出或者写入的必须为字符串，其他形式需转为字符串。  
首先，写入文件：


```python
f = open('file.txt', 'w')
```


```python
type(f)
```




    _io.TextIOWrapper




```python
f.write('This is a test \nand another test')
```




    32




```python
f.close()
```

读出文件：


```python
f = open('file.txt', 'r')
```


```python
s = f.read()
```


```python
print(s)
```

    This is a test 
    and another test
    


```python
f.close()
```

迭代文件：


```python
f = open('file.txt', 'r')
```


```python
for line in f:
    print(line)
```

    This is a test 
    
    and another test
    


```python
f.close()
```

文件读写模式：  
* `r` : 只读
* `w` : 只写，如果文件已经存在，会覆盖之前的内容
* `a` : 添加，不覆盖之前的内容
* `r+/w+` : 读和写
* `b` : 二进制模式  

## 关闭文件  
在Python中，如果一个打开的文件不再被其他变量引用时，它会自动关闭这个文件。  
所以正常情况下，如果一个文件正常被关闭了，忘记调用文件的 `close` 方法不会有什么问题。  
关闭文件可以保证内容已经被写入文件，而不关闭可能会出现意想不到的结果：  


```python
f = open('newfile.txt', 'w')
f.write('You should close the file!')
g = open('newfile.txt', 'r')
print(repr(g.read()))
```

    ''
    

虽然这里写了内容，但是在关闭之前，这个内容并没有被写入磁盘。  
使用循环写入的内容也并不完整：


```python
f = open('newfile.txt','w')
for i in range(1000):
    f.write('You should close the file: ' + str(i) + '\n')

g = open('newfile.txt', 'r')
print(g.read())
f.close()
g.close()
```

    You should close the file: 0
    You should close the file: 1
    You should close the file: 2


```python
import os
os.remove('newfile.txt')
```

出现异常时的读写：


```python
f = open('newfile.txt','w')
for i in range(3000):
    x = 1.0 / (i - 1000)
    f.write('hello world: ' + str(i) + '\n')
```


    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    <ipython-input-25-8dc1cc9b29ec> in <module>()
          1 f = open('newfile.txt','w')
          2 for i in range(3000):
    ----> 3     x = 1.0 / (i - 1000)
          4     f.write('hello world: ' + str(i) + '\n')
    

    ZeroDivisionError: float division by zero



```python
g = open('newfile.txt', 'r')
print(g.read())
g.close()
```

    hello world: 0
    hello world: 1

    
    

## with方法  
事实上，Python提供了一个安全的方法，当 `with` 代码块的内容结束后，Python会自动调用它的 `close` 方法，确保读写的安全：


```python
with open('newfile.txt','w') as f:
    for i in range(3000):
        x = 1.0 / (i - 1000)
        f.write('hello world: ' + str(i) + '\n')
```


    ---------------------------------------------------------------------------

    ZeroDivisionError                         Traceback (most recent call last)

    <ipython-input-28-9d2a70065b27> in <module>()
          1 with open('newfile.txt','w') as f:
          2     for i in range(3000):
    ----> 3         x = 1.0 / (i - 1000)
          4         f.write('hello world: ' + str(i) + '\n')
    

    ZeroDivisionError: float division by zero



```python
g = open('newfile.txt', 'r')
print(g.read())
g.close()
```

    hello world: 0
    hello world: 1
    hello world: 2
    
    


```python
import os 
os.remove('newfile.txt')
```
