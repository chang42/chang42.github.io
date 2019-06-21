
# 控制流

## if/elif/else 判断语句  
判断，基于一定的条件，决定是否要执行特定的一段代码。  
```
if <condition 1>:
    <statement 1>
    <statement 2>
elif <condition 2>: 
    <statements>
else:
    <statements>
```


```python
if 2 * 2 == 4:
    print('Obvious!')
```

    Obvious!
    

Python使用缩进来区分不同的代码块主体。Ipython shell会自动缩进。


```python
a = 1

if a % 2 == 0:
    print('Even')
elif a % 2 == 1:
    print('Odd')
else:
    print('Not a Integer')
```

    Odd
    

## for 循环  
```
for <variable> in <sequence>:
    <indented block of code>
```
`for`循环会遍历完`<sequence>`中所有元素为止。


```python
for i in range(4):
    print(i)
```

    0
    1
    2
    3
    


```python
words = set(['cool', 'powerful', 'readable'])
for word in words:
    print('Python is %s' % word)
```

    Python is cool
    Python is powerful
    Python is readable
    

## while/break/continue 循环

```
while <condition>:
    <statesments>
```
Python会循环执行`<statesments>`，直到不满足`<condition>`为止。


```python
z = 1 + 1j
while abs(z) < 100:
    z = z**2 + 1
z
```




    (-134+352j)



遇到`break`的时候，程序会跳出循环，不管循环条件是不是满足：


```python
z = 1 +1j

while abs(z) < 100:
    if z.imag == 0:
        break
    z = z**2 + 1
z
```




    (-134+352j)



遇到`continue`的时候，程序会返回到循环的最开始重新执行。


```python
a = [1, 0, 2, 4]
for element in a:
    if element == 0:
        continue
    print(1. / element)
```

    1.0
    0.5
    0.25
    

## 列表推导式   
可以用循环来生成列表


```python
[i**2 for i in range(4)]
```




    [0, 1, 4, 9]



可以在列表推导式中加入条件进行筛选


```python
squares = [i**2 for i in range(4) if i < 3]
squares
```




    [0, 1, 4]



利用推导式生成集合和字典：


```python
square_set = {i**2 for i in range(4) if i < 3}
square_set
```

    {0, 1, 4}
    


```python
square_dict = {i : i**2 for i in range(4) if i < 3}
square_dict
```




    {0: 0, 1: 1, 2: 4}



枚举


```python
for i in range(0, len(squares)):
    print((i, squares[i]))
```

    (0, 0)
    (1, 1)
    (2, 4)
    


```python
for index, item in enumerate(squares):
    print((index, item))
```

    (0, 0)
    (1, 1)
    (2, 4)
    

字典循环


```python
for key, val in sorted(square_dict.items()):
    print('key: %s has value: %s' % (key, val))
```

    key: 0 has value: 0
    key: 1 has value: 1
    key: 2 has value: 4
    
