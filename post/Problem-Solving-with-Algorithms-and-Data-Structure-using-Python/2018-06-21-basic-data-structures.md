
# 基本数据结构 Basic Data Structures   
## 3.2 线性数据结构(Linear Structures)  
四种数据形式：栈(stacks)、队列(queues)、双端队列(deques)、列表(lists)——数据集合各项的顺序由添加和删除的方式决定。如果添加某项后，该项处于先前添加元素和后添加元素之间的位置，则该数据集合称为线性数据结构(linear data structures)。  
线性数据结构有两个端，添加和删除项的方式是区分线性数据结构和其他数据结构的依据，特别是添加和删除发生的位置。

## 3.3 栈(stacks)  
### 3.3.1 栈(stacks) 
栈(stacks)为限制添加和删除项只能在同一端的项的有序集合，该端称为“顶(top)”，与顶对应端的称为“底(base)”。栈有时又称作LIFO（last-in first-out, 后进先出），最后被添加的项最先被删除，它基于项在集合中的沉淀时间长短做排序，新来的项在上面，旧的项在底端，可以想象桌子上的一摞书。  
![image](http://interactivepython.org/courselib/static/pythonds/_images/bookstack2.png)
![image](http://interactivepython.org/courselib/static/pythonds/_images/primitive.png)
![image](http://interactivepython.org/courselib/static/pythonds/_images/simplereversal.png)  
举个例子，每个 web 浏览器都有一个“返回”按钮，当浏览网页时，这些网页（网址）被放置在一个栈中，当前网页在顶部，第一个查看的网页在底部，如果按“返回”按钮，将按相反的顺序浏览刚才的页面。

### 3.3.2 栈的抽象数据类型  
栈的操作有：  
* `Stack()` creates a new stack that is empty. It needs no parameters and returns an empty stack.
* `push(item)` adds a new item to the top of the stack. It needs the item and returns nothing.
* `pop()` removes the top item from the stack. It needs no parameters and returns the item. The stack is modified.
* `peek()` returns the top item from the stack but does not remove it. It needs no parameters. The stack is not modified.
* `isEmpty()` tests to see whether the stack is empty. It needs no parameters and returns a boolean value.
* `size()` returns the number of items on the stack. It needs no parameters and returns an integer.  
  
|Stack Operation|Stack Contents|Return Value|
|:-:|:-:|:-:|
|s.isEmpty()|[]|True|
|s.push(4)|[4]||
|s.push('dog')|[4,'dog']||
|s.peek()|[4,'dog']|'dog'|
|s.push(True)|[4,'dog',True]||
|s.size()|[4,'dog',True]|3|
|s.isEmpty()|[4,'dog',True]|False|
|s.push(8.4)|[4,'dog',True,8.4]|| 
|s.pop()|[4,'dog',True]|8.4|
|s.pop()|[4,'dog']|True|
|s.size()|[4,'dog']|2|  

### 3.3.3 Python中的栈实现  
在Python以及任何一种其他面向对象的程序语言中，抽象数据结构（栈等）的实现方式是创建新的类(class)，栈的操作通过方法(methods)实现。此外，为了实现作为元素集合的栈数据结构，可以利用Python本身提供的原始集合(primitive collections)——列表(list)。  
Python的列表类中，提供了一些列的有序集合机制和方法，我们所需要做的仅是选择列表的哪一端作为栈的顶和底，栈的操作也可以通过列表的`pop`和`append`方法实现。  


```python
class Stack:
     def __init__(self):
         self.items = []

     def isEmpty(self):
         return self.items == []

     def push(self, item):
         self.items.append(item)

     def pop(self):
         return self.items.pop()

     def peek(self):
         return self.items[len(self.items)-1]

     def size(self):
         return len(self.items)
        
```


```python
s = Stack()
```


```python
print(s.isEmpty())
```

    True



```python
s.push(4)
```


```python
s.push('dog')
```


```python
print(s.peek())
```

    dog



```python
s.push(True)
```


```python
print(s.size())
```

    3



```python
print(s.isEmpty())
```

    False



```python
s.push(8.4)
```


```python
print(s.pop())
```

    8.4



```python
print(s.pop())
```

    True



```python
print(s.size())
```

    2


如果选择列表的开始作为栈的顶，列表操作`pop`和`append`就不能直接拿来用作栈的方法。


```python
class Stack:
     def __init__(self):
         self.items = []

     def isEmpty(self):
         return self.items == []

     def push(self, item):
         self.items.insert(0,item)

     def pop(self):
         return self.items.pop(0)

     def peek(self):
         return self.items[0]
```


```python
s = Stack()
```


```python
s.push('hello')
```


```python
s.push('true')
```


```python
print(s.pop())
```

    true


可以看到以上两种方式实现的栈都可行，但是考虑到`append` 和 `pop()` 操作的复杂度为 $\mathcal{O}(1)$，`insert(0)` 和 `pop(0)` 操作的复杂度为 $\mathcal{O}(n)$，他们的性能是有区别的。

### 3.3.4 简单括号匹配  
现在我们用栈来解决一个实际的计算机问题，在基本的数学运算式中，括号必定是相互嵌套成对出现的，现在我们面临的挑战是如何设计一套算法来从左到右地读取一组括号字符串，判断它是否相互嵌套对应，观察下面的图，从左至右操作符号时，最近的开符号必定对应下一个闭符号，同样，初始的开符号对应最后的闭符号，而闭符号的匹配顺序与此相反，从符号串的中间开始匹配。  
![image](http://interactivepython.org/courselib/static/pythonds/_images/simpleparcheck.png)  
而栈结构正适用于存储这些括号，创建一个空的栈，从左至右操作符号字符串，如果为开符号，将其放进栈里，直到对应的闭符号出现，如果为闭符号，就会从栈中弹出。只要弹出的开符号与闭符号对应，则栈会一直保持平衡，直到符号字符串结束，栈会为空。  


```python
from pythonds.basic.stack import Stack

def parChecker(symbolString):
    s = Stack()
    balanced = True
    index = 0
    while index < len(symbolString) and balanced:
        symbol = symbolString[index]
        if symbol == '(':
            s.push(symbol)
        else:
            s.pop()
            
        index = index + 1
        
    if balanced and s.isEmpty():
        return True
    else:
        return False
```


```python
print(parChecker('((()))'))
```

    True



```python
print(parChecker('((())'))
```

    False



```python
print(parChecker(')'))
```


    ---------------------------------------------------------------------------

    IndexError                                Traceback (most recent call last)

    <ipython-input-28-d2656d4c42e6> in <module>()
    ----> 1 print(parChecker(')'))
    

    <ipython-input-24-7aabc5b1574a> in parChecker(symbolString)
         10             s.push(symbol)
         11         else:
    ---> 12             s.pop()
         13 
         14         index = index + 1


    ~/miniconda3/lib/python3.6/site-packages/pythonds/basic/stack.py in pop(self)
         16 
         17     def pop(self):
    ---> 18         return self.items.pop()
         19 
         20     def peek(self):


    IndexError: pop from empty list


### 3.3.5 通用符号匹配  
下面我们介绍一种更通用的场景，包含了圆括号'()'、方括号'[]'和花括号'{}'。这样情况会复杂很多，不仅要考虑符号是否相互嵌套对应，还需要考虑是否是同一种类型的符号，这里要用到`match()`方法。


```python
from pythonds.basic.stack import Stack

def parChecker(symbolString):
    s = Stack()
    balanced = True
    index = 0
    while index < len(symbolString) and balanced:
        symbol = symbolString[index]
        if symbol in "([{":
            s.push(symbol)
        else:
            if s.isEmpty():
                balanced = False
            else:
                top = s.pop()
                if not matches(top, symbol):
                    balanced = False
        index = index + 1
    if balanced and s.isEmpty():
        return True
    else:
        return False
    
def matches(open, close):
    opens = "([{"
    closers = ")]}"
    return opens.index(open) == closers.index(close)
```


```python
print(parChecker('{{([][])}()}'))
```

    True



```python
print(parChecker('[{()]'))
```

    False


### 3.3.6 进制转换  
计算机是以二进制的形式存储数据，这里我们看一下如何利用“除2法”将整数转变为二进制数。  
“除2法”首先假设一个大于0的十进制整数，连续地除以2取余，如果余数为1，则计该位为1，如果为0，则计该位为0，商继续除以2取余，这样第一个余数会位于字节序列的最后位置，依次类推，可以看下面的图示。
![image](http://interactivepython.org/courselib/static/pythonds/_images/dectobin.png)  
  
十进制($233_{10}$)：  
$2\times10^2+3\times10^1+3\times10^0$  
二进制($11101001_2$)：  
$1\times2^7+1\times2^6+1\times2^5+0\times2^4+1\times2^3+0\times2^2+0\times2^1+1\times2^0$  
八进制($351_8$)：  
$3\times8^2+5\times8^1+1\times8^0$  
十六进制($E9_{16}$)：  
$14\times16^1+9\times16^0$  


```python
from pythonds.basic.stack import Stack

def divideBy2(decNumber):
    remstack = Stack()
    
    while decNumber > 0:
        rem = decNumber % 2
        remstack.push(rem)
        decNumber = decNumber // 2
        
    binString = ''
    while not remstack.isEmpty():
        binString = binString + str(remstack.pop())
        
    return binString
```


```python
print(divideBy2(233))
```

    11101001



```python
from pythonds.basic.stack import Stack

def baseConverter(decNumber, base):
    digits = "0123456789ABCDEF"
    
    remstack = Stack()
    
    while decNumber > 0:
        rem = decNumber % base
        remstack.push(rem)
        decNumber = decNumber // base
        
    newString = ""
    while not remstack.isEmpty():
        newString = newString + digits[remstack.pop()]
        
    return newString
```


```python
print(baseConverter(233, 8))
```

    351



```python
print(baseConverter(233, 16))
```

    E9


## 3.4 中缀、前缀和后缀表示法（Infix, Prefix and Postfix Expression）  
对于一个数学表达式：$(A+B)*C+D$，我们很容易分辨其运算的先后顺序，因为不同的运算具有不同的优先级，这种表示方式为中缀表达式，但是对于计算机而言，它需要确切地知道运算操作的顺序，可以通过全括号表示来区分运算的操作顺序，例如上面的式子可以表示为：$(((A+B)*C)+D)$，这样做的好处是不用考虑运算操作的优先级。  
除此之外，还有两种非常重要的表示形式——前缀（prefix）和后缀（postfix）表示，又称波兰（Polish notation）和逆波兰（Reverse Polish notation）表示，前缀表示的特点是操作符置于操作数的前面，即：$+ * + A B C D $；后缀表示的特点是所有操作符置于操作数的后面，即：$A B + C * D + $。这样做的好处是不再需要括号了，运算的顺序仅通过表达顺序决定，减少了标记符号的使用。  
  
|Infix Expression|Prefix Expression|Postfix Expression|
|:-:|:-:|:-:|
|A+B|+AB|AB+|
|A+B*C|+A*BC|ABC*|
|(A+B)*C|*+ABC|AB+C*|
|A+B*C+D|++A*BCD|ABC*+D+|
|(A+B)*(C+D)|*+AB+CD|AB+CD+*|
|A*B+C*D|*+AB+CD|AB*CD*+|
|A+B+C+D|+++ABCD|AB+C+D+|

### 3.4.1 中缀表示与前缀和后缀表示的转换  
中缀表示转换为前缀和后缀表示首先需要做的是写出数学运算表达式的全括号表示，再将括号内的运算符放到外面并去掉括号，如下面的图所示：  
![image.png](http://interactivepython.org/courselib/static/pythonds/_images/complexmove.png)

### 3.4.2 通用中缀-后缀转换  
通过上面的例子我们可以看到，中缀-后缀转换操作数的位置不变，仅仅是操作符的位置发生改变。假设中缀表达式为以空格为分隔符的记号字符串，操作符记号为 “*, /, +, -” 以及左右括号 “()” ，操作数为“A, B, C, D, ...”，则产生后缀表示的程序为：  
1. 创建一个空的栈 `opstack` 来保存操作符，创建一个空的输出列表；
2. 通过字符串方法 `split` 将中缀字符串转变为列表；
3. 从左至右依次扫描记号列表；
 * 如果记号为操作数，将其添加到输出列表的末端；
 * 如果记号为左括号，将其放进栈 `opstack` 中；
 * 如果记号为右括号，弹出栈 `opstack` 中的元素，直到对应的左括号被移除，将弹出的我操作符依次添加到输出列表的末端；
 * 如果记号为操作符 *, /, +, - ，将其放进栈 `opstack` 中，但是，当栈 `opstack` 顶已经存在的操作符优先级高于或等于其时，该操作符首先被弹出，并添加到输出列表的末端，然后再将其放入栈中；
4. 当对输入的表达式操作完成后，检查栈 `opstack` ，移除栈 `opstack` 中剩余的操作符并添加到输出列表的末端。  
  
如下图对$A*B+C*D$的操作示例：  

![image.png](http://interactivepython.org/courselib/static/pythonds/_images/intopost.png)  
  
代码示例：


```python
from pythonds.basic.stack import Stack

def infixToPostfix(infixexpr):
    # Use a dictionary called prec to hold the precedence values for the operators
    prec = {}
    prec["*"] = 3
    prec["/"] = 3
    prec["+"] = 2
    prec["-"] = 2
    prec["("] = 1
    # Create an empty `stack` called opstack for keeping operators
    opStack = Stack()
    # Create an empty list for output
    postfixList = []
    # Convert the input infix string to a list by using the string method `split`
    tokenList = infixexpr.split()
    
    # Scan the token list from left to right
    for token in tokenList:
        # If the token is an operand, append it to the end of the output list
        if token in "ABCDEFGHIJKLMNOPQRSTUVWXYZ" or token in "0123456789":
            postfixList.append(token)
        # If the token is a left parenthesis, push it on the `opstack`
        elif token == '(':
            opStack.push(token)
        # If the token is a right parenthesis, pop the opstack until the corresponding left parenthesis is removed. 
        # Append each operator to the end of the output list
        elif token == ')':
            topToken = opStack.pop()
            while topToken != '(':
                postfixList.append(topToken)
                topToken = opStack.pop()
        # If the token is an operator, *, /, +, or -, push it on the opstack. 
        # However, first remove any operators already on the opstack that have higher or equal precedence 
        # and append them to the output list.
        else:
            while (not opStack.isEmpty()) and \
                (prec[opStack.peek()] >= prec[token]):
                    postfixList.append(opStack.pop())
            opStack.push(token)
            
    # When the input expression has been completely processed, check the opstack. 
    # Any operators still on the stack can be removed and appended to the end of the output list      
    while not opStack.isEmpty():
        postfixList.append(opStack.pop())
    return "".join(postfixList)
```


```python
infixToPostfix("A * B + C * D")
```




    'AB*CD*+'




```python
infixToPostfix("( A + B ) * C - ( D - E ) * ( F + G )")
```




    'AB+C*DE-FG+*-'



### 3.4.3 后缀表达式求值  
伪代码：  
* while有输入符号   
    * 读入下一个符号X  
    * IF X是一个操作数 
        *入栈
    * ELSE IF X是一个操作符 
        *有一个先验的表格给出该操作符需要n个参数
        * IF堆栈中少于n个操作数 
            * （错误） 用户没有输入足够的操作数
        *Else，n个操作数出栈
        * 计算操作符。
        * 将计算所得的值入栈
* IF栈内只有一个值 
    * 这个值就是整个计算式的结果
* ELSE多于一个值 
    * （错误） 用户输入了多余的操作数  
  
下图是计算后缀表达式$4\ 5\ 6\ *\ +$的示例：  
![image.png](http://interactivepython.org/courselib/static/pythonds/_images/evalpostfix1.png)  
  
下表给出了该后缀表达式从左至右求值的过程，堆栈栏给出了中间值，用于跟踪算法。
  
|输入|操作|堆栈|注释|
|:-:|:-:|:-:|:-:|
|4|入栈|4||
|5|入栈|4, 5||
|6|入栈|4, 5, 6||
|*|乘法运算|4, 30|(5, 6)出栈；将结果(30)入栈|
|+|加法运算|34|(4, 30)出栈；将结果(34)入栈|  
  
假设后缀表达式为以空格为分隔符的记号字符串，操作符记号为 “*, /, +, -” ，操作数为一位整数，则后缀表示求值的程序为：  
1. 创建一个空的栈 `operandStack`；
2. 通过字符串方法 `split` 将中缀字符串转变为列表；
3. 从左至右依次扫描记号列表；
    * 如果记号为操作数，将其从字符转换为整数，将其值放入栈 `operandStack` 中；
    * 如果记号为操作符 *, /, +, - ，它两个操作数，从栈 `operandStack` 中弹出两个值，首先弹出的是第二个操作数，随后弹出的是第一个操作数，进行数学运算，将得到的结果放回栈 `operandStack` 中；
4. 当对输入的表达式操作完成后，结果在栈 `operandStack` 中，弹出结果并返回。  
  
代码示例：


```python
from pythonds.basic.stack import Stack

def postfixEval(postfixExpr):
    operandStack = Stack()
    tokenList = postfixExpr.split()
    
    for token in tokenList:
        if token in "0123456789":
            operandStack.push(int(token))
        else:
            operand2 = operandStack.pop()
            operand1 = operandStack.pop()
            result = doMath(token, operand1, operand2)
            operandStack.push(result)
    return operandStack.pop()

def doMath(op, op1, op2):
    if op == "*":
        return op1 * op2
    elif op == "/":
        return op1 / op2
    elif op == "+":
        return op1 + op2
    else:
        return op1 - op2
```


```python
postfixEval('7 8 + 3 2 + /')
```




    3.0




```python
postfixEval('5 1 2 + 4 * + 3 −')
```




    14




```python
postfixEval('4 5 6 * +')
```




    34



## 3.5 队列（Queue）  
### 3.5.1 队列（Queue）  
和栈一样，队列（queue）也是项的有序集合，但是，添加新的项在其一端进行，该端称为队尾（rear），删除项在另一端进行，该端称为队头（front）。当一个元素在队尾进入队列以后，一直超队头移动，直到它成为下一个被删除的元素为止。最先被添加进队列的项位于集合的末端，在集合中存活时间最长的项位于队头，该特性称为先进先出（FIFO, first-in first-out/first-come first-seved）。  
![image.png](http://interactivepython.org/courselib/static/pythonds/_images/basicqueue.png)  
生活中我们经常排队，在队列中，只有一个方向进另外一个方向出，人们也别想插队，上图便是Python语言中的简单队列对象示意。在计算机科学场景中，操作系统使用不同的队列来控制进程，对于进程处理的时间先后安排便是基于一个队列算法——如何尽快地执行程序和尽可能多地服务更多的用户。  

### 3.5.2 队列的抽象数据类型  
队列是结构化的项的有序集合，其插入在队尾一端进行而删除在队头一端进行，其具有先进先出特性，队列的操作有：  
* `Queue()` 创建一个新的空队列，不需要任何参数，并返回一个空队列。
* `enqueue(item)` 在队尾添加新的项，需要一个 `item` 作为参数，无返回。
* `dequeue()` 移除队头的项，不需要参数，并返回 `item` ，队列被修改。
* `isEmpty()` 检查队列是否为空，不需要参数，返回一个布尔值。
* `size()` 返回队列中项的数目，不需要参数，返回一个整数。 
  
|Queue Operation|Queue Contents|Return Value|
|:-:|:-:|:-:|
|q.isEmpty()|[]|True|
|q.enqueue(4)|[4]||
|q.enqueue('dog')|['dog', 4]||
|q.enqueue(True)|[True,'dog', 4]||
|q.size()|[True, 'dog', 4]|3|
|q.isEmpty()|[True, 'dog', 4]|False|
|q.enqueue(8.4)|[8.4, True, 'dog, 4]||
|q.dequeue()|[8.4, True, 'dog']|4|
|q.dequeue()|[8.4, True]|'dog'|
|q.size()|[8.4, True]|2|

### 3.5.3 Python中的队列实现  
同样的，抽象数据类型队列可以通过创建一个新的类实现，利用Python本身的列表集合构建队列的内部表示。  
首先，我们需要决定队列的队头和队尾，在下面的表示中，队尾为列表的0位置，这样我们就可以利用列表的 `insert` 函数在队尾添加新元素，复杂度为$\mathcal{O}(n)$， `pop`操作用来移除队头的元素，复杂度为$\mathcal{O}(1)$。  


```python
class Queue:
    def __init__(self):
        self.items = []
        
    def isEmpty(self):
        return self.items == []
    
    def enqueue(self, item):
        self.items.insert(0, item)
        
    def dequeue(self):
        return self.items.pop()
    
    def size(self):
        return len(self.items)
```


```python
q = Queue()
```


```python
q.isEmpty()
```




    False




```python
q.enqueue(4)
```


```python
q.enqueue('dog')
```


```python
q.size()
```




    2




```python
q.enqueue(True)
```


```python
q.enqueue(8.4)
```


```python
q.size()
```




    4




```python
q.dequeue()
```




    4




```python
q.dequeue()
```




    'dog'




```python
q.size()
```




    2



### 3.5.4 队列模拟——击鼓传花（Hot potato）
让我们一个实际生活中运用队列FIFO原则的例子，在击鼓传花游戏中人们围坐成一圈，花（或者其他信物）被挨个传递，当鼓点突然停止时，停止传递，花落在谁那里就会被淘汰，直到剩下最后一个人  
![image.png](http://interactivepython.org/courselib/static/pythonds/_images/hotpotato.png)  
另外一个著名的问题约瑟夫环（Josephus problem or Josephus permutation），人们站在一个等待被处决的圈子里。从圆圈中的指定点开始计数，并沿指定方向围绕圆圈进行。在跳过指定数量的人之后，淘汰这个人。对剩下的人重复该过程，从下一个人开始，朝同一方向跳过相同数量的人，直到只剩下一个人。  
我们利用Python程序来解决这个问题，开始输入人名和数字用于计数中间跳过人数，最后返回经过循环最终剩下的人，我们利用队列来实现，假设Bill位于队头手上拿着山芋，程序通过让Bill出队，再入队的方式将山芋传递给下一个位于队头的人David，直到循环给定的次数，永久地移除队头的人，一直循环直到剩下最后一个人。  
![image.png](http://interactivepython.org/courselib/static/pythonds/_images/namequeue.png)


```python
from pythonds.basic.queue import Queue

def hotPotato(nameList, num):
    simQueue = Queue()
    for name in nameList:
        simQueue.enqueue(name)
        
    while simQueue.size() > 1:
        for i in range(num):
            simQueue.enqueue(simQueue.dequeue())
            
        simQueue.dequeue()
        
    return simQueue.dequeue()
```


```python
hotPotato(["Bill", "David", "Susan", "Jane", "Kent", "Brad"], 7)
```




    'Susan'



### 3.5.5 队列模拟——打印任务队列  
我们来考虑这样一个问题，一个机房里的学生将打印任务提交给共享打印机，打印任务以队列形式按照先进先出惯例执行。这里面有很多问题值得研究，其一是打印机是否能够处理确定数量的任务。  
考虑下面这种情况，在每天的任意时间，平均会有10个学生在机房，这些学生通常会在该时间段内提交两次打印任务，这样打印任务的长度为1到20页，但是机房的打印机已经陈旧不堪，每分钟仅能打印10张草稿级别的页面，如果切换到更高的打印质量，每分钟就只能打印5张，这样学生就需要等待更长的时间，我们来如何选择页面速率呢？  
我们从中抽象出一个模型——由学生、打印任务和打印机三个元素构建，当学生提交任务，就把它放到待处理列表中——打印机的打印任务队列，当打印机完成一项任务，它就会查看打印队列中是否还有打印任务，而我们所关心的是学生提交的任务被执行需等待的时间，这等于打印任务存在于队列中的平均时间。  
![image.png](http://interactivepython.org/courselib/static/pythonds/_images/simulationsetup.png)  
该模型需要一些概率的知识，例如，学生会打印1到20页长度的论文，如果1到20页长度的论文近似等可能出现，这样打印任务的实际长度可以用1到20中的随机数来模拟，即1到20的任意长度出现的机率相同。  
如果有10个学生在机房，这些学生通常会在一小时内平均提交两次打印任务，那么任意给定时间点创建打印任务概率是多少？我们可以考虑任务时间比，每小时20个任务意味着每180秒一个任务：  
$\frac{20 tasks}{1 hours}\times\frac{1 hours}{60 minutes}\frac{1 minute}{60 seconds} = \frac{1 task}{180 seconds}$  
用1到180之间的随机数来模拟每秒钟打印任务创建的几率，如果数字是180，可以说该任务已经被创建，需要注意的是，可能会一下子创建许多任务，或者需要等待一段时间才有任务。这就是模拟的实质，需要用已知的参数来尽可能真实地反映实际情况。

#### 主要模拟流程  
1. 创建一个打印队列，每一个任务都会指定一个时间戳，开始时队列为空。
2. 每一秒（`CurrentSecond`）：
    * 如果一个新的打印任务被创建，将其放入队列中，以当前时间为时间戳。
    * 如果打印机空闲且任务等待处理：
        * 从打印队列中移出一个任务，交给打印机。
        * 从 `CurrentSecond` 中减去时间戳计算任务的等待时间。
        * 将该任务的等待时间放入列表中等待后处理。
        * 基于打印任务的页数，得出所需时间。
    * 打印机需要一秒的时间打印，需要从任务所需时间内扣除。
    * 如果任务已经完成，即所需时间将为0，打印机处于空闲状态。
3. 模拟完成后，从生成的等待时间列表中的计算平均待处理时间。

#### Python实现  
我们创建类—— `Printer` , `Task` , `PrintQueue` 来模拟上述的三个真实对象。`Printer` 类需要追踪当前打印机是否有任务，如果有，则处于忙碌状态，所需时间以任务中的页数计。构造器同样允许初始化每分钟打印页数配置。而 `tick` 方法逐步递减间隔时间直到任务完成将打印机设置为空闲状态。


```python
class Printer:
    def __init__(self, ppm):
        self.pagerate = ppm
        self.currentTask = None
        self.timeRemaining = 0
        
    # The tick method decrements the internal timer and sets the printer to idle if the task is completed
    def tick(self):
        if self.currentTask != None:
            self.timeRemaining = self.timeRemaining - 1
            if self.timeRemaining <= 0:
                self.currentTask = None
    
    # If the task has been completed, in other words the time required has reached zero, the printer is no longer busy
    def busy(self):
        if self.currentTask != None:
            return True
        else:
            return False
    
    # Based on the number of pages in the print task, figure out how much time will be required
    def startNext(self, newtask):
        self.currentTask = newtask
        self.timeRemaining = newtask.getPages()*60/self.pagerate
```

`Task` 类表示一个单独的打印任务，利用Python `random` 模块中的 `randrange` 函数产生1到20间的随机数模拟任务长度，每个任务还需要保存一个时间戳来计算待处理时间，时间戳表示任务被创建后待在打印队列中的时间， `waitTime` 方法用来检索在打印开始前在队列中的时间消耗。


```python
import random

class Task:
    def __init__(self, time):
        self.timeStamp = time
        self.pages = random.randrange(1, 21)
    
    # This timestamp will represent the time that the task was created and placed in the printer queue
    def getStamp(self):
        return self.timeStamp
    
    # A random number generator will provide a length of task from 1 to 20 pages
    def getPages(self):
        return self.pages
    
    # The waitTime method can then be used to retrieve the amount of time spent in the queue before printing begins
    def waitTime(self, currentTime):
        return currentTime - self.timeStamp
```

主模拟程序如下所示， `printQueue` 对象是我们现有抽象数据结构队列的实例， `newPrintTask` 辅助方程返回布尔值，决定是否创建新的打印任务，我们仍然利用 `random` 模块中的 `randrange` 函数产生1到180间的随机数，打印任务每180秒提交一次，通过从随机产生整数列中选取180来模拟随机事件。


```python
from pythonds.basic.queue import Queue

import random

def simulation(numSeconds, pagesPerMinute):
    
    labPrinter = Printer(pagesPerMinute)
    printQueue = Queue()
    waitingTimes = []
    
    for currentSecond in range(numSeconds):
        if newPrintTask():
            task = Task(currentSecond)
            printQueue.enqueue(task)
            
        if (not labPrinter.busy()) and (not printQueue.isEmpty()):
            nextTask = printQueue.dequeue()
            waitingTimes.append(nextTask.waitTime(currentSecond))
            labPrinter.startNext(nextTask)
            
        labPrinter.tick()
        
    averageWait = sum(waitingTimes)/len(waitingTimes)
    print("Average wait %6.2f secs %3d tasks remaining."%(averageWait, printQueue.size()))
    
def newPrintTask():
    num = random.randrange(1, 181)
    if num == 180:
        return True
    else:
        return False
```


```python
for i in range(10):
    simulation(3600, 5)
```

    Average wait  61.30 secs   0 tasks remaining.
    Average wait 193.88 secs   2 tasks remaining.
    Average wait 219.33 secs   0 tasks remaining.
    Average wait   0.77 secs   1 tasks remaining.
    Average wait  40.50 secs   1 tasks remaining.
    Average wait 171.29 secs   1 tasks remaining.
    Average wait 106.86 secs   0 tasks remaining.
    Average wait  40.64 secs   0 tasks remaining.
    Average wait 136.42 secs   0 tasks remaining.
    Average wait  71.72 secs   0 tasks remaining.



```python
for i in range(10):
    simulation(3600, 10)
```

    Average wait  25.93 secs   0 tasks remaining.
    Average wait  21.82 secs   0 tasks remaining.
    Average wait  10.84 secs   0 tasks remaining.
    Average wait   9.82 secs   0 tasks remaining.
    Average wait  72.33 secs   4 tasks remaining.
    Average wait  11.00 secs   0 tasks remaining.
    Average wait   8.14 secs   0 tasks remaining.
    Average wait  12.00 secs   0 tasks remaining.
    Average wait  10.36 secs   0 tasks remaining.
    Average wait  19.96 secs   0 tasks remaining.


我们分别以5页/分和10页/分的页面打印速率模拟打印机运行1小时（3600秒）后的状态，可以看到，提高页面打印速率，平均等待时间更短，而且所有打印任务的都完成的概率也更高，因此减慢速率提高打印质量并不是一个好的策略，因为学生的平均等待时间更长了。

## 3.6 双端队列（Deque）
### 3.6.1 双端队列（Deque）
双端队列（deque）是类似于队列的有序项集合，它也有两个端，队头和队尾，项在集合中位置不变，但它与队列相区别的是其添加和删除项的非限制特性——新的项在队头和队尾都可以添加，同时，已有项在两端都可以被删除，在某种意义上，该混合线性结构在单一数据结构框架下提供了栈和队列的所有特性。虽然如此，但其并不需要遵循栈或队列所必须遵循的LIFO或FIFO顺序，而是取决于使用者的操作。  
![image.png](http://interactivepython.org/courselib/static/pythonds/_images/basicdeque.png)  
### 3.6.2 双端队列的抽象数据类  
双端队列是结构化的项的有序集合，其项的插入和删除可以在队尾和队头任意一端进行，双端队列的操作有：  
* `Deque()` 创建一个新的空双端队列，不需要参数返回空双端队列。
* `addFront(item)` 在双端队列的队头添加新项，需要参数 `item` 无返回。
* `addRear(item)` 在双端队列的队尾添加新项，需要参数 `item` 无返回。
* `removeFront()` 从队头删除项，不需要参数，返回该项，双端队列被修改。
* `removeRear()` 从队尾删除项，不需要参数，返回该项，双端队列被修改。
* `isEmpty()` 检查双端队列是否为空，不需要参数，返回一个布尔值。
* `size()` 返回双端队列中项的数目，不需要参数，返回一个整数。
  
创建一个空双端队列 `d` ，对其进行操作及相应结果显示如下：  
  
|Deque Opreation|Deque Contents|Return Value|
|:-:|:-:|:-:|
|d.isEmpty()|[]|True|
|d.addRear(4)|[4]||
|d.addRear('dog')|['dog', 4]||
|d.addFront('cat')|['dog', 4, 'cat]||
|d.addFront(True)|['dog', 4, 'cat', True]||
|d.size()|['dog', 4, 'cat', True]|4|
|d.isEmpty()|['dog', 4, 'cat', True]|False|
|d.addRear(8.4)|[8.4, 'dog', 4, 'cat', True]||
|d.romoveRear()|['dog', 4, 'cat', True]|8.4|
|d.removeFront()|['dog', 4, 'cat]|True|
  
### 3.6.3 双端队列的Python实现  
和之前一样，抽象数据类型双端队列可以通过创建一个新的类实现，利用Python本身的列表的方法集合构建具体的双端队列，当中最重要的是要谨记实现过程中所规定的队头和队尾位置。假设双端队列的队头位于列表的0位置。


```python
class Deque:
    def __init__(self):
        self.items = []
        
    def isEmpty(self):
        return self.items == []
    
    def addFront(self, item):
        self.items.append(item)
        
    def addRear(self, item):
        self.items.insert(0, item)
        
    def removeFront(self):
        return self.items.pop()
        
    def removeRear(self):
        return self.items.pop(0)
        
    def size(self):
        return len(self.items)
```

在 `removeFront` 中，我们利用 `pop`方法删除列表中的最后一个元素，复杂度为$\mathcal{O}(1)$，而在 `removeRear` 中，利用`pop(0)` 来删除列表的第一个元素，复杂度为$\mathcal{O}(n)$。同样，在 `addRear` 中的利用 `insert` 方法，复杂度为$\mathcal{O}(n)$，而  `append` 则是在列表末端添加元素，复杂度为$\mathcal{O}(1)$。


```python
d = Deque()
```


```python
d.isEmpty()
```




    True




```python
d.addRear(4)
```


```python
d.addRear('dog')
```


```python
d.addFront('cat')
```


```python
d.addFront(True)
```


```python
d.size()
```




    4




```python
d.isEmpty()
```




    False




```python
d.addRear(8.4)
```


```python
d.removeRear()
```




    8.4




```python
d.removeFront()
```




    True



### 3.6.4 双端队列应用——回文检测（Palindrome-Checker）  
我们可以利用双端队列数据结构来解决经典的回文问题，回文即一个字符串从正向或反向读都是一样的，例如 radar，toot，madam，我们可以构建一个算法来检查输入的字符串字母是否回文。  
![image.png](http://interactivepython.org/courselib/static/pythonds/_images/palindromesetup.png)  
利用双端队列来存储字符串的字母，从左至右操作字符串，在双端队列的队尾依次添加每个字母，在这一点上，双端队列表现为队列特性，然后，利用双端队列的双端可操作性，同时从双端队列的队头和队尾移出项，然后比较，如果相同，则继续操作，直到双端随列为空或只剩一个元素，这取决于其长度是奇数还是偶数。具体实现如下：


```python
from pythonds.basic.deque import Deque

def palChecker(aString):
    charDeque = Deque()
    
    for char in aString:
        charDeque.addRear(char)
        
    stillEqual = True
    
    while charDeque.size() > 1 and stillEqual:
        first = charDeque.removeFront()
        last = charDeque.removeRear()
        
        if first != last:
            stillEqual = False
            
    return stillEqual
```


```python
palChecker('asdfghjkl')
```




    False




```python
palChecker('radar')
```




    True



## 3.7 列表（List）  
### 3.7.1 无序列表（Unordered List）
在之前的讨论中，我们利用Python中的列表实现了一些抽象数据类型，足见列表是一简单强大的集合机制，同时提供了各式的操作，但是并不是每一种程序语言中，都会有列表集合，因此，我们需要手动实现一下它。  
列表是项的集合，项在集合中的相对位置保持不变，它可被视为是无序的，且无重复项。列表通过逗号来分隔。  
无序列表的一些操作有：  
* `List()` 创建一个新的空列表，不需要参数，返回一个空列表。
* `add(item)` 向列表添加新的项，需要参数 `item` 无返回，且需假设列表中不存在该项。
* `remove(item)` 从列表中删除该项，需要参数 `item` 且列表被修改，需假设列表中已存在该项。
* `search(item)` 在列表中搜寻该项，需要参数 `item` 返回一个布尔值。
* `isEmpty()` 检查列表是否为空。不需要参数，返回一个布尔值。
* `size()` 返回列表内项的数目，不需参数，返回一个整数。
* `append(item)` 在列表的末端添加项，使它称为集合的最后项，需要参数 `item` 返回空，且需假设列表中不存在该项。
* `index(item)` 返回该项在列表中的位置，需要参数 `item` 返回索引，需假设列表中已存在该项。
* `insert(pos, item)` 在指定位置添加项，需要参数 `item` 返回索引，需假设列表中已存在该项。
* `pop()` 删除列表的最后一项并返回该项，不需要参数，返回该项，需假设列表至少包含一个项。
* `pop(pos)` 删除指定位置的项，需要参数 `position` 返回该项，需假设列表中已存在该项。  
  
### 3.7.2 无序列表的的实现：链表（Linked Lists）  
![image](http://interactivepython.org/courselib/static/pythonds/_images/idea.png)  
![image](http://interactivepython.org/courselib/static/pythonds/_images/idea2.png)  
如上图中，各项位置随机，如果各项之间的相对位置可以表示成各项之间的相对链接，这样只需知道第一项的位置，就可以知道其他各项的位置，第一项称为列表的表头（head），最后一项无下一项，指向空。之所以这样规定是因为如果列表在内存中连续存储，则插入和删除会移动列表的部分或全部项，线性开销会很大。  
#### `Node` 类  
结点（node）是建立链表表示的基石，每一个结点对象含有两点信息：第一，结点必须包含列表项本身，称作结点的数据域；此外，还需包含指向下一结点的链接。以下是Python实现：


```python
class Node:
    def __init__(self, initdata):
        self.data = initdata
        self.next = None
        
    def getData(self):
        return self.data
    
    def getNext(self):
        return self.next
    
    def setData(self, newdata):
        self.data = wendata
        
    def setNext(self, newnext):
        self.next = newnext
```


```python
temp = Node(93)
```


```python
temp.getData()
```




    93




```python
temp.getNext()
```

为了构建一个结点，需要提供结点的初始值，同时，其还包含有链接和修改当前和指向下一项链接的方法。  
![image](http://interactivepython.org/courselib/static/pythonds/_images/node.png)  
![image](http://interactivepython.org/courselib/static/pythonds/_images/node2.png)  
Python中的特殊reference value `None` 在结点类和链表中起非常重要作用，引用 `None` 意味着再没有结点了，需要注意的是一开始结点的下一项便被设置为 `None` ，因此该做法被称为“结点接地”，用标准的接地符号来表示对 `None` 的引用。

#### 无序列表类  
如上所述，无序列表可以构建为结点集合，确定的链接到下一个，只要知道第一个结点，其他各项便可通过指向下一个的链接找到，考虑到这一点， `UnorderedList` 类需要保持与第一个结点的链接，注意每个列表对象都保持对表头的链接。


```python
class UnorderedList:
    
    def __init__(self):
        self.head = None
```

`None` 用于声明表头没有任何指向，一开始讨论的列表可以表示成如下所示的链表，链表的表头指向含有列表第一项的第一个结点，该结点保存有指向下一个结点的链接。注意链表类本身不包含任何节点对象，相反，它只包含对链接结构中第一个节点的单个链接。  
![image](http://interactivepython.org/courselib/static/pythonds/_images/initlinkedlist.png)  
![image](http://interactivepython.org/courselib/static/pythonds/_images/linkedlist.png)  
`isEmpty` 方法查看链表的表头是否指向 `None` ，通过 `self.head==None` 判断，只有在链表中没有节点时才为真，由于新链表为空，因此构造函数和空检查必须彼此一致，这显示了使用引用 None 来表示链接结构结尾的优点。在 Python 中，`None` 可以与任何引用进行比较，如果两个链接都指向相同的对象，则它们是相等的。


```python
def isEmpty(self):
    return self.head == None
```

由于链表时无序的，新添加的项相对于链表中其他项的具体位置并不重要，它可以在任何地方，链表结构只有一个入口——链表表头，添加的新项只需位于表头，将已有项链接到它上面位于其后就可以了。


```python
def add(self, item):
    temp = Node(item)
    temp.setNext(self.head)
    self.head = temp
```

![image](http://interactivepython.org/courselib/static/pythonds/_images/addtohead.png)  
如上图所示，链表的每一项属于结点对象，`temp = Node(item)` 行创建了一个以 `item` 为值的新结点，然后把他链接到已有的结构上，需要两步：第一步，`temp.setNext(self.head)` 行改变新结点的 `next` 链接到链表的之前首结点上，然后 `self.head = temp` 行将该结点设为表头。  
链表其他的方法 `size`， `search`， `remove`，都基于被称为链表遍历（linked list traversal）的技术。遍历操作即有序地访问每一个结点，利用一个外部链接，从链表第一个结点开始，通过“遍历”外部链接访问每一个结点。  
通过遍历链表计数结点的个数实现 `size` 方法，外部的链接命名为 `current` 且初始化为链表表头，在操作开始，没有遇到任何结点时，计数为0。依次移动 `current` 直到链表结束（None），每当 `current` 移动到新结点，计数就加1，最后迭代结束返回计数值。  
![image](http://interactivepython.org/courselib/static/pythonds/_images/traversal.png)


```python
def size(self):
    current = self.head
    count = 0
    while current != None:
        count = count + 1
        current = self.getNext()
        
    return count
```

`search` 方法通过问链表中的每一个结点，查看其存储的值是否匹配我们所需要寻找的值。在`search` 方法的实现中，利用布尔值变量 `found` 定位所需要寻找的项，初始值设为 `False` ，迭代依次进行直到找到所需要寻找的项，初始值设为 `True` 。  
![image](http://interactivepython.org/courselib/static/pythonds/_images/search.png)


```python
def search(self, item):
    current = self.head
    found = False
    while current != None:
        if current.getData() == item:
            found = True
        else:
            current = current.getNext()
            
    return found
```

`remove` 方法需要两个逻辑步骤：第一，遍历链表找到所需要删除的项，类似于 `search` 方法；找到它以后，删除，想要删除该结点，必须修改前一个结点的链接，将他链接到 `current` 指向的结点的下一个结点，但是，在链表中无法返回， 因为 `current` 指向的结点已位于该结点之后。我们可以使用两个外部链接来解决该困境，增加一个 `previous` 链接，紧随 `current` ，当 `current` 停在需要被删除的结点处时， `previous` 位于链表中需要被修改的结点处。  
![image](http://interactivepython.org/courselib/static/pythonds/_images/removeinit.png)
![image](http://interactivepython.org/courselib/static/pythonds/_images/prevcurr.png)


```python
def remove(self, item):
    # assign initial values to the two references, 
    # current starts out at the list head as in the other traversal examples, 
    # previous, however, is assumed to always travel one node behind current
    current = self.head
    previous = None
    found = False
    while not found:
        # whether the item stored in the current node is the item we wish to remove
        # If so, found can be set to True
        if current.getData() == item:
            found = True
        # If we do not find the item, previous and current must both be moved one node ahead
        else:
            previous = current
            current = current.getNext()
    
    # previous starts out with a value of None since there is no node before the head
    if previous == None:
        self.head = current.getNext()
    else:
        previous.setNext(current.getNext())
```

一旦完成搜寻步骤，就需要删除链表中的该结点，如下图所示。当然，还有一种特殊情况就是，删除的结点为链表的第一个结点，`current` 指向链表的第一个结点，此时 `previous` 为 `None`。先前我们已经声明 `previous` 指向需要被修改的结点，而在这种情况下，链表的表头会被修改。  
![image](http://interactivepython.org/courselib/static/pythonds/_images/remove.png)
![image](http://interactivepython.org/courselib/static/pythonds/_images/remove2.png)  
`if previous == None:` 行检查是否处于上述情况，如果 `previous` 没有移动，则当布尔值 `found` 为 `True` 时其值一直为 `None` ，`self.head = current.getNext()` 行通过删除首结点，链表表头被修改为链接到当前结点的下一个结点。当然，如果 `previous` 不为 `None` ，则要删除的结点位于链表结构的下方，该情况下， `previous` 指向下一个链接需要改变的结点。`previous.setNext(current.getNext())` 行利用 `setNext` 方法从 `previous` 中完成删除操作。注意在上述两种情况下，链接的指向改为指向 `current.getNext()` 。  

### 3.7.3 有序队列的抽象数据结构  
如果之前所述的整数序列为有序的列表（递增序列），例如写成17，26，31，54，77，93，数值最小的项17位于列表的首位，数值最大的项93位于列表的末位，有序列表结构即所含项的次序遵循某些基本特性依次排列的集合，例如常见的有升序或降序排列，而其基本的比较操作已经事先确定。有序列表的操作有：  
* `OrderedList()` 创建一个新的空有序列表，不需要参数，返回一个空列表。
* `add(item)` 向列表添加新的项，需要参数 `item` 无返回，且需假设列表中不存在该项。
* `remove(item)` 从列表中删除该项，需要参数 `item` 且列表被修改，需假设列表中已存在该项。
* `search(item)` 在列表中搜寻该项，需要参数 `item` 返回一个布尔值。
* `isEmpty()` 检查列表是否为空。不需要参数，返回一个布尔值。
* `size()` 返回列表内项的数目，不需参数，返回一个整数。
* `index(item)` 返回该项在列表中的位置，需要参数 `item` 返回索引，需假设列表中已存在该项。
* `insert(pos, item)` 在指定位置添加项，需要参数 `item` 返回索引，需假设列表中已存在该项。
* `pop()` 删除列表的最后一项并返回该项，不需要参数，返回该项，需假设列表至少包含一个项。
* `pop(pos)` 删除指定位置的项，需要参数 `position` 返回该项，需假设列表中已存在该项。 
  
### 3.7.4 有序列表的Python实现  
首先我们要谨记有序列表所含项的次序遵循某些基本特性依次排列，同样，用结点和链接结构来表示项的相对位置：  
![image](http://interactivepython.org/courselib/static/pythonds/_images/orderlinkedlist.png)  
`OrderedList` 类的实现上，可以利用与无序列表相同的一些方法，首先，空列表表示为列表表头链接到 `None`。


```python
class OrderedList:
    def __init__(self):
        self.head = None
```

`isEmpty` 和 `size` 方法都是处理结点的个数无需处理结点内的值，因此，使用与无序列表相同的表示，同样的， `remove` 方法仍然是找到需删除的项，让后将其前后的结点链接起来。然而，剩下的两个 `search` 和 `add` 方法需要一些修改。  
在 `search` 方法中，遍历结点寻找要查找的项的路数依然有效，只是当需要寻找的项不在列表内时，会稍有区别，无序列表需要遍历完列表内所有结点然后返回，但是由于有序列表是有序排列的，可以相比更快的结束。  
例如如下图所示，在一个有序列表中寻找45，遍历时，首先对比第一个结点17，不是需要找的项，然后移动到下一个结点26，然后继续，如果按照这个策略，会遍历所有结点，最后返回 `False` ，但是我们看到因为列表是有序排列的，当移动到结点54的时候，虽然其不是所要查找的项，但是由于其值已经大于45，且其后面的结点值一定也大于45，所以，在该位置就可以结束查找返回 `False` 了。  
![image](http://interactivepython.org/courselib/static/pythonds/_images/orderedsearch.png)   
在无序列表 `search` 方法下增加一个初始值为 `False` 的布尔变量 `stop` ，当结点内的值大于所需查找的值时， `stop` 的值设为 `True` 。


```python
def serch(self, item):
    current = self.head
    found = False
    stop = False
    while current != None and not found and not stop:
        if current.getData() == item:
            found = True
        else:
            if current.getData() > item:
                stop = True
            else:
                current = current.getNext()
                
    return found
```

在 `add` 方法中，相对需要修改的幅度比较大，在无序列表中，只需在表头增加新的结点就可以了，但在有序列表中远不这么简单，还需要我们首先定位要将其放置的位置。  
例如我们想要将31放入一个有序列表17，26，54，77，93中， `add` 方法首先需要通过遍历查找确定它应该被放到26与54之间，即 `current` 值大于所需添加的值（还有一种情况是已经遍历完表内所有的结点，`current` 变成 `None` ）。  
![image](http://interactivepython.org/courselib/static/pythonds/_images/linkedlistinsert.png)  
我们同样需要一个 `previous` 链接，因为 `current` 已经位于需要编辑结点之面。


```python
def add(self, item):
    # set up the two external references
    current = self.head
    previous = None
    stop = False
    # The condition allows the iteration to continue as long as there are more nodes and the value in the current node is not larger than the item
    while current != None and not stop:
        if current.getData() > item:
            stop = True
        # allow previous to follow one node behind current every time through the iteration
        else:
            previous = current
            current = current.getNext()
    
    temp = Node(item)
    # the new node will be added at the beginning of the linked list
    if previous == None:
        temp.setNext(self.head)
        self.head = temp
    # the new node will be added at some place in the middle 
    else:
        temp.setNext(current)
        previous.setNext(temp)
```

### 3.7.5 链表分析  
我们可以通过所需的遍历次数来分析操作的复杂度，考虑一个拥有n个结点的链表， `isEmpty` 仅需要一步来检查表头链接是否为空，因此其复杂度为$\mathcal{O}(1)$， `size` 方法通常来讲需要n步，因为如果不遍历一遍链表就无法知道其含有多少结点，因此 `length` 的复杂度是$\mathcal{O}(n)$。在无序列表中添加新的项仅仅需要在表头添加新的结点，复杂度为$\mathcal{O}(1)$。对于有序列表， `search`，`remove` 和 `add` 需要遍历操作，平均需要遍历一般的结点，考虑最坏的情况需要遍历完整个列表，其复杂度为$\mathcal{O}(n)$。  
当然，我们注意到这些表示的性能与Python真实的列表性能不同，其实Python的列表并不是基于链表实现的而是基于数组（array）的概念。

## 3.8 总结  
* 线性数据结构保持其数据为有序的形式。
* 栈数据结构，具有LIFO和有序的特性，基本操作有：`push`, `pop`, `isEmpty`。
* 队列数据结构，具有FIFO和有序的特性，基本操作有：`enqueue`, `dequeue`, `isEmpty`。
* 前缀、中缀和后缀都可于书写表达式。
* 栈结构用于设计表达式求值和变换非常合适。
* 栈拥有反转特性。
* 队列可以辅助构建计时模拟。
* 随机数生成器可以模拟实际情况，以解答“what if”类的问题。
* 双端队列为拥有类似栈和队列的混合表现的结构，基本操作有：`addFront`, `addRear`, `removeFront`, `removeRear`,`isEmpty`。
* 列表为项相对位置确定的项集合。
* 链表表示无需物理内存的前提下保证了逻辑顺序。
* 编辑链表的表头需要特别注意。


```python

```
