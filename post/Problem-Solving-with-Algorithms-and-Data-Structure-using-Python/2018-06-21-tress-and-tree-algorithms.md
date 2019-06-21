
# 6 树 Trees and Tree Algorithms  

## 6.1 树的示例  
线性数据结构：堆栈、队列。  
树(tree)是另外一种常见的数据结构。  

## 6.2 术语和定义 Vocabulary and Definitions  
### 术语 Vocabulary  
* 节点(Node)  
树的基本部分，节点的名字叫做"key"，附加信息称为"payload"。  
* 边(Edge)  
边连接两个节点，除了根节点，每一个节点都有一个入边，若干个出边。
* 根(Root)  
唯一没有入边的节点。  
* 路径(Path) 
边连接的有序节点。  
* 子节点(Children)  
拥有相同来源节点的节点集合。
* 母节点(Parent)  
子节点的来源节点。  
* 兄弟节点(Sibling)  
拥有相同母节点的各子节点为兄弟节点。
* 子树(Subtree)  
母节点以及子孙节点构成的节点与边的集合。  
* 叶节点(Leaf Node)  
没有子节点的节点。  
* 层(Leavel)  
从根节点到该节点的路径所包含的边的数目。
* 高(Height)  
所有节点中的最高层称为树的高。  

### 定义 Definitions  

定义1： 树由一系列节点和连接一对节点的边的集合组成，树的一些特性：  
* 有一个节点被设置为根节点。  
* 除了根节点，每一个节点n被从节点p出来的边连接，p为n的母节点。  
* 根节点到每一个节点的路径唯一。  
* 如果一棵树中的每一个节点最多拥有两个子节点，该树结构称为二叉树(binary tree)。  
    
定义2： 每一个树结构或为空或为根节点以及零个或若干个子树组成，该子树亦为树结构。（递归定义）

## 6.3 列表的列表表示 List of Lists Representation  
列表树结构中，例表第一项表示根节点，第二项表示左面子树，第三项表示右面子树，如图所示：
![smalltree.png](http://interactivepython.org/courselib/static/pythonds/_images/smalltree.png)  
下面示例用列表表示树结构：


```python
myTree = ['a', 
          ['b', 
           ['d', 
            [], 
            []], 
           ['e', 
            [], 
            []]
          ], 
          ['c', 
           ['f', 
            [], 
            []], 
           []]]
```

上面的列表本身为递归结构，其能更好的表示子树依附于树状结构，而子树有一个根节点值和和两个空列表叶节点；另外其还可以产生拥更多子树的树结构。


```python
print(myTree)
```

    ['a', ['b', ['d', [], []], ['e', [], []]], ['c', ['f', [], []], []]]



```python
print('left subtree = ', myTree[1])
```

    left subtree =  ['b', ['d', [], []], ['e', [], []]]



```python
print('root = ', myTree[0])
```

    root = a



```python
print('right subtree = ', myTree[2])
```

    right subtree =  ['c', ['f', [], []], []]


构建`BinaryTree`函数来产生一个由根节点和两个空子列表构成的列表：


```python
def BinaryTree(r):
    return [r, [], []]
```

添加左面的子树，需要将新列表插入根列表的第二个位置，如果该位置不为空的话，需要保留并将其下推作为新添加列表的左子节点，如下所示：


```python
def insertLeft(root, newBranch):
    t = root.pop(1)
    if len(t) > 1:
        root.insert(1, [newBranch, t, []])
    else:
        root.insert(1, [newBranch, [], []])
    return root
```

函数`insertRight`与`insertLeft`类似：


```python
def insertRight(root, newBranch):
    t = root.pop(2)
    if len(t) > 1:
        root.insert(2, [newBranch, [], t])
    else:
        root.insert(2, [newBranch, [], []])
    return root
```

还需要一些函数获取和设置根和左右子树的值，来完成树生成函数：


```python
def getRootVal(root):
    return root[0]

def setRootVal(root, newVal):
    root[0] = newVal
    
def getLeftChild(root):
    return root[1]

def getRightChild(root):
    return root[2]
```


```python
r = BinaryTree(3)
```


```python
r
```




    [3, [], []]




```python
insertLeft(r, 4)
```




    [3, [4, [], []], []]




```python
insertLeft(r, 5)
```




    [3, [5, [4, [], []], []], []]




```python
insertRight(r, 6)
```




    [3, [5, [4, [], []], []], [6, [], []]]




```python
insertRight(r, 7)
```




    [3, [5, [4, [], []], []], [7, [], [6, [], []]]]




```python
l = getLeftChild(r)
```


```python
l
```




    [5, [4, [], []], []]




```python
setRootVal(l, 9)
```


```python
l
```




    [9, [4, [], []], []]




```python
insertLeft(l, 11)
```




    [9, [11, [4, [], []], []], []]




```python
r
```




    [3, [9, [11, [4, [], []], []], []], [7, [], [6, [], []]]]




```python
getRightChild(getRightChild(r))
```




    [6, [], []]



![tree_ex.png](http://interactivepython.org/courselib/static/pythonds/_images/tree_ex.png)


```python
x = BinaryTree('a')
insertLeft(x, 'b')
insertRight(getLeftChild(x), 'd')
insertRight(x, 'f')
insertRight(x, 'c')
insertLeft(getRightChild(x), 'e')
x
```




    ['a', ['b', [], ['d', [], []]], ['c', ['e', [], []], ['f', [], []]]]



## 6.4 节点和引用 Nodes and References  
第二种表示树的方法可以利用节点和引用，定义一个类，拥有关于根和左右子树的属性，其结构如下图所示，该表示方法遵循面向对象编程的范例，因此以后的一些章节中多用该表示方法。  
![treerecs.png](http://interactivepython.org/courselib/static/pythonds/_images/treerecs.png)  
下面的示例中定义了`BinaryTree`类，其中`left`和`right`属性引用到其他`BinaryTree`类的实例。例如，在树中插入一个新的左子树，我们首先创建一个新的`BinaryTree`实例，然后将`self.leftChild`引用指向它的根节点。


```python
class BinaryTree:
    def __init__(self, rootObj):
        self.key = rootObj
        self.leftChild = None
        self.rightChild = None
```

在上面的示例中，构造函数将对象存储在根节点，根节点可以链接到任何对象，在之前的例子中，将节点的名称作为根值。利用该方法需要6个`BinaryTree`类示例来表示上图。  
在根节点下构建新的子树，利用`insertLeft`或`insertRight`方法，首先创建新的二叉树对象，然后将之前根节点的`left`属性链接到新的对象上，需要注意的是：1. 当没有已存的左子树，就直接将节点插入到树中；2. 如果有已存的左子树，插入新的节点，并将原来的子树推向下一层。


```python
def insertLeft(self, newNode):
    if self.leftChild == None:
        self.leftChild = BinaryTree(newNode)
    else:
        t = BinaryTree(newNode)
        t.leftChild = self.leftChild
        self.leftChild = t
```


```python
def insertRight(self, newNode):
    if self.rightChild == None:
        self.leftChild = BinaryTree(newNode)
    else:
        t = BinaryTree(newNode)
        t.rightChild = self.rightChild
        self.rightChild = t
```

还需要一些额外的方法来完善二叉树数据结构


```python
def getRightChild(self):
    return self.rightChild

def getLeftChild(self):
    return self.leftChild

def setRootVal(self, obj):
    self.key = obj
    
def getRootVal(self):
    return self.key
```

我们利用以上的方法来构建一个树结构，可以看到根节点的所有左右子树本身也是`BinaryTree`类实例，这允许我们将二叉树的任意子树也看作二叉树。


```python
class BinaryTree:
    def __init__(self, rootObj):
        self.key = rootObj
        self.leftChild = None
        self.rightChild = None
        
    def insertLeft(self, newNode):
        if self.leftChild == None:
            self.leftChild = BinaryTree(newNode)
        else:
            t = BinaryTree(newNode)
            t.leftChild = self.leftChild
            self.leftChild = t
            
    def insertRight(self, newNode):
        if self.rightChild == None:
            self.rightChild = BinaryTree(newNode)
        else:
            t = BinaryTree(newNode)
            t.rightChild = self.rightChild
            self.rightChild = t
            
    def getRightChild(self):
        return self.rightChild

    def getLeftChild(self):
        return self.leftChild

    def setRootVal(self, obj):
        self.key = obj

    def getRootVal(self):
        return self.key
```


```python
r = BinaryTree('a')
```


```python
print(r.getRootVal())
```

    a



```python
print(r.getLeftChild())
```

    None



```python
r.insertLeft('b')
```


```python
print(r.getLeftChild())
```

    <__main__.BinaryTree object at 0x7f4e341310b8>



```python
print(r.getLeftChild().getRootVal())
```

    b



```python
r.insertRight('c')
```


```python
print(r.getRightChild())
```

    <__main__.BinaryTree object at 0x7f4e34131128>



```python
print(r.getRightChild().getRootVal())
```

    c



```python
r.getRightChild().setRootVal('hello')
```


```python
print(r.getRightChild().getRootVal())
```

    hello


![](http://interactivepython.org/courselib/static/pythonds/_images/tree_ex.png)


```python
tree = BinaryTree('a')
tree.insertLeft('b')
tree.getLeftChild().insertRight('d')
tree.insertRight('c')
tree.getRightChild().insertLeft('e')
tree.getRightChild().insertRight('f')
```

## 6.5 语法树 Parse Tree  
语法树可以用来表示句子或者数学表达式的结构。
句子的等级结构，将句子表示成树结构有助于我们利用子树来研究句子的特定部分：  
![nlParse.png](http://interactivepython.org/courselib/static/pythonds/_images/nlParse.png)  
数学表达式`((7+3)*(5-2))`的语法树结构：  
![meParse.png](http://interactivepython.org/courselib/static/pythonds/_images/meParse.png)  
树的等级结构帮助我们理解表达式求值的次序，首先得出加操作和减操作子树的值，然后得出其相乘的结果。利用树结构，可以将整个子树的子节点的结果替换到子树的根节点：  
![meSimple.png](http://interactivepython.org/courselib/static/pythonds/_images/meSimple.png)  
在下面的部分，从三个方面更详尽的介绍语法树：  
* 如何构建括号表示数学表达式的语法树。  
* 如何求值语法树中表达式。  
* 如何从语法树中逆向构建原始数学表达式。  
  
构建语法树需要将表达式字符拆分成符号列表，需要考虑四种符号：左括号，右括号，操作符，操作值。读取表达式时，遇到左括号就创建一个与该表达式相关的新树，相反，遇到右括号意味着完成表达式操作；操作值为树的叶节点，也是操作符的子节点，每一个操作符都有左右子节点，定义规则如下：  
* 如果当前符号为`'('`，添加一个新的节点作为当前节点的左子节点，其之下为后代节点；  
* 如果当前符号为`['+', '-', '/', '*']`，将当前节点的根值置为该，并添加一个新的节点为当前节点的右子节点，其之下为后代节点；  
* 如果当前的符号为数字，将当前节点的根值置为该数字并返回母结点；  
* 如果当前符号为`')'`，返回当前节点的母结点。  
  
对于表达式`(3+(4*5))`将其解析为符号列表：`[(', '3', '+', '(', '4', '*', '5' ,')',')']`，首先从一个空的根节点开始进行相应操作：  
![buildExp1.png](http://interactivepython.org/courselib/static/pythonds/_images/buildExp1.png)  
![buildExp2.png](http://interactivepython.org/courselib/static/pythonds/_images/buildExp2.png)  
![buildExp3.png](http://interactivepython.org/courselib/static/pythonds/_images/buildExp3.png)  
![buildExp4.png](http://interactivepython.org/courselib/static/pythonds/_images/buildExp3.png)  
![buildExp5.png](http://interactivepython.org/courselib/static/pythonds/_images/buildExp3.png)  
![buildExp6.png](http://interactivepython.org/courselib/static/pythonds/_images/buildExp6.png)  
![buildExp7.png](http://interactivepython.org/courselib/static/pythonds/_images/buildExp7.png)  
![buildExp8.png](http://interactivepython.org/courselib/static/pythonds/_images/buildExp8.png)  
分步详解：  
1. 创建新的空树；
2. 读取第一个符号`'('`，根据规则1，创建一个新节点作为根节点的左子节点，当前节点为该左子节点；
3. 读取下一个符号`'3'`，根据规则3，将当前节点的根值置为`3`，并返回其母节点；
4. 读取下一个符号`'+'`，根据规则2，将当前节点的根值置为`+`，创建一个新的节点作为其右子节点，当前节点为该右子节点；
5. 读取下一个符号`'('`，根据规则1，，创建一个新节点作为根节点的左子节点，当前节点为该左子节点；
6. 读取下一个符号`'4'`，根据规则3，将当前节点的根值置为`4`，并返回其母节点；  
7. 读取下一个符号`'*'`，根据规则2，将当前节点的根值置为`*`，创建一个新的节点作为其右子节点，当前节点为该右子节点；  
8. 读取下一个符号`'5'`，根据规则3，将当前节点的根值置为`5`，并返回其母节点；  
9. 读取下一个符号`')'`，根据规则4，并返回其母节点`*`，当前节点为该母结点；
10. 读取下一个符号`')'`，根据规则4，并返回其母节点`+`，当前节点为该母结点，此时，该节点无母节点，完成操作。  
  
在上面的例子中，毫无疑问需要时刻清楚当前节点以及其母节点，前述的树类提供了获取子节点的方法`getLeftChild`和`getRightChild`，但是如何追迹其母节点？可以利用堆栈来转置树结构，当需要在当前节点下继承一个子节点，将当前节点推入栈中，而当需要返回当前节点的母节点时，从栈中弹出其母节点。  
利用`Stack`和`BinaryTree`操作，我们写出Python函数来创建语法树：


```python
from pythonds.basic.stack import Stack
from pythonds.trees.binaryTree import BinaryTree
```


```python
def buildParseTree(fpexp):
    fplist = fpexp.split()
    pStack = Stack()
    eTree = BinaryTree('')
    pStack.push(eTree)
    currentTree = eTree
    for i in fplist:
        # If the current token is a '(', add a new node as the left child of the current node, and descend to the left child.
        if i == '(':
            currentTree.insertLeft('')
            pStack.push(currentTree)
            currentTree = currentTree.getLeftChild()
        # If the current token is a number, set the root value of the current node to the number and return to the parent.
        elif i not in ['+', '-', '*', '/', ')']:
            currentTree.setRootVal(int(i))
            parent = pStack.pop()
            currentTree = parent
        # If the current token is in the list ['+','-','/','*'], set the root value of the current node to the operator represented by the current token. Add a new node as the right child of the current node and descend to the right child.
        elif i in ['+', '-', '*', '/']:
            currentTree.setRootVal(i)
            currentTree.insertRight('')
            pStack.push(currentTree)
            currentTree = currentTree.getRightChild()
        # If the current token is a ')', go to the parent of the current node.
        elif i == ')':
            currentTree = pStack.pop()
        # If we get a token from the list that we do not recognize.
        else:
            raise ValueError
    return eTree
```


```python
pt = buildParseTree("( ( 10 + 5 ) * 3 )")
```

接下来构建`evaluate`函数递归求各个子树的值来得到语法树的运算结果，首先确定递归的base case——由于语法树的叶节点为数值对象，因此只需返回叶节点的值。`evaluate`函数的递归可以逐层检查当前节点的左右子节点以移向叶节点，然后将母节点中的运算符作用于递归返回的子节点数值。具体代码示例如下，首先获取当前节点的左右子节点引用，如果左右子节点的值为`None`，则当前节点为叶节点；如果当前节点非叶节点，获取当前节点中的操作符，作用于递归返回的左右子节点数值。


```python
import operator
```

利用字典(dictionary)将键`'+', '-', '*',  '/'`与Python中的`operator`模块相应函数对应，Python中的`operator`模块提供了一些常用运算符的函数形式，即`function(param1,param2)`。


```python
def evaluate(parseTree):
    opers = {'+':operator.add, '-':operator.sub, '*':operator.mul, '/':operator.truediv}
    
    leftC = parseTree.getLeftChild()
    rightC = parseTree.getRightChild()
    
    if leftC and rightC:
        fn = opers[parseTree.getRootVal()]
        return fn(evaluate(leftC), evaluate(rightC))
    else:
        return parseTree.getRootVal()
```

利用`evaluate`函数求语法树`(3+(4∗5))`的运算结果，首先将整个语法树的根节点传给参数`parseTree`，随后得到其左右子节点的引用，确认其是否存在，行9为递归调用，查看根节点的运算符`'+'`，映射到`operator.add`函数，其两个参数均为`evaluate`函数递归调用，第一个递归调用作用于左子树，该结点没有左右子节点，为叶节点，返回其存的数值对象`'3'`，接下第二个递归调用求右子树的运算结果，右子树的根节点有左右子节点，且其根节点所存值为运算符`'*'`，再次调用`evaluate`函数作用于其左右子节点，由于其左右子节点均为叶节点，返回其存的数值对象`'4'`和`'5'`作为母节点操作符`'*'`的参数，并返回其映射函数`operate.mul(4, 5)`的结果`'20'`，而`'20'`又作为之前母节点操作符`'+'`的另外一个参数，最后返回其映射函数`operate.add(3, 20)`的结果`'23'`，此即为表达式`(3+(4∗5))`的运算结果。

## 6.6 树的遍历 Tree Traversals  
访问树结构中的所有节点称为遍历(traversal)，根据各节点访问次序的不同，有三种常用的遍历类型——先序(preorder)、中序(inorder)和后序(postorder)。  
先序(preorder)  
在先序遍历中，首先访问根节点，之后递归地先序遍历左子树，随后递归地先序遍历右子树。  
中序(inorder)  
在中序遍历中，首先递归地中序遍历左子树，之后访问根节点，最后递归的遍历右子树。  
后序(postorder)  
在后序遍历中，先递归地后序遍历左右子树，随后访问根节点。  
![booktree.png](http://interactivepython.org/courselib/static/pythonds/_images/booktree.png)  
将一本书表示成上图所示的树结构，`book`是根节点，`chapter`为根节点的子节点，`section`为该章节的子节点，我们将树简化为二叉树。  
先序遍历：Book->Chapter 1->Section 1.1->Chapter 1->Section 1.2->Section 1.2.1->Section 1.2.2->Chapter 1->Book->Chapter 2->Section 2.1->Chapter 2->Section 2.2->Section 2.2.1->Section 2.2.2  
我们看到先序遍历的代码是如此的简练，恰恰是因为其递归结构。但究竟是将其表示为树结构的函数形式还是树结构的方法更适合？首先来看树结构作为参数的函数形式：


```python
def preorder(tree):
    if tree != None:
        print(tree.getRootVAl())
        preorder(tree.getLeftChild())
        preorder(tree.getRightChild())
```

由于递归的base case仅仅是检查树是否存在，函数形式的表达非常简洁——如果参数`tree`为`None`，函数无操作返回。  
再将`preorder`表示为`BinaryTree`类的方法，仅需要将参数`tree`替换为`self`就可以了，当然，basecase也需要相应修改——在递归调用`preorder`前首先检查左右子节点是否存在。


```python
def preorder(self):
    print(self.key)
    if self.leftChild:
        self.leftChild.preorder()
    if self.rightChild:
        self.leftChild.preorder()
```

通过比较貌似函数表示更适合，如果很少去遍历整个树，在大多数情况下，在完成其他任务目的时会需要用到几种基本遍历型式中的一个。而且在随后还将会看到`postorder`遍历型式与之前的语法树求值代码相近，因此后面都将用外部函数形式来写这几种遍历。  
后序遍历函数`postorder`如下所示，与先序遍历`preorder`类似，除了将`print`的调用置于函数的末尾。


```python
def postorder(tree):
    if tree != None:
        postorder(tree.getLeftChild())
        postorder(tree.getRightChild())
        print(tree.getRootVal())
```

其实在之前的语法树求值中我们已经利用了后序遍历类型——首先求值左子树以及右子树，然后将根节点的操作符作用到它们上。将之前的求值函数重写为与`preorder`代码类似的形式：


```python
def postordereval(tree):
    opers = {'+':operator.add, '-':operator.sub, '*':operator.mul, '/':operator.truediv}
    res1 = None
    res2 = None
    if tree != None:
        res1 = postordereval(tree.getLeftChild())
        res2 = postordereval(tree.getRightChild())
        if res1 and res2:
            return opers[tree.getRootVal()](res1, res2)
        else:
            return tree.getRootVal()
```

上面的代码中，最后返回了根值，最后将行6和行7返回的值用行9的操作符计算。  
最后来看中序遍历(inorder traversal)——首先中序遍历左子树，然后根节点，最后中序遍历右子树：


```python
def inorder(tree):
    if tree != None:
        inorder(tree.getLeftChild())
        print(tree.getRootVal())
        inorder(tree.getRightChild())
```

可以看到以上所有的遍历函数仅改变了`print`声明相对于递归调用的位置。如果仅通过中序遍历语法树，只能得到原来表达式的无括号形式，将中序遍历函数做简单修改就可以用它返回全括号表达式——在递归调用左子树前打印左括号，在递归调用右子树后打印右括号。


```python
def printexp(tree):
    sVal = ""
    if tree != None:
        sVal = '(' + printexp(tree.getLeftChild())
        sVal = sVal + str(tree.getRootVal())
        sVal = sVal + printexp(tree.getRightChild()) + ')'
    return sVal
```

运行上面的`printexp`函数可以看到其在所有的数字两边都加上了括号，显然有些是没有必要的，我们可以通过修改函数`printexp`来移除多余的括号。


```python
printexp(pt)
```




    '(((10)+(5))*(3))'




```python
def printExpWoPare(tree):
    sVal = ""
    l = ""
    r = ""
    if tree != None :
        if tree.getLeftChild() != None:
            l = '('
        sVal = l + printExpWoPare(tree.getLeftChild())
        sVal = sVal + str(tree.getRootVal())
        sVal = sVal + printExpWoPare(tree.getRightChild())
        if tree.getRightChild() != None:
            r = ')'
        sVal = sVal + r
    return sVal
```


```python
printExpWoPare(pt)
```




    '((10+5)*3)'



## 6.7 二叉堆的优先队列  Priority Queues with Binary Heaps  
优先队列(Priority Queues)是队列的变种，有点类似于可以从前端剔除元素的队列，当然，优先队列中项的逻辑次序取决于其优先级，优先级最高的项位于队列前端，低优先级的队列位于队列后端。当向优先队列中添加项时，新的项可能会一直排到最前端。优先队列数据结构在图算法中非常有用。  
我们可以想到利用排序和列表等一系列简单的方法来表示优先队列，然而插入列表的复杂度是$\mathcal{O}(n)$，排序列表的复杂度是$\mathcal{O}(n\log n)$。此外还有更好的表示方式——二叉堆(Binary Heap)，其项入队和出队操作的复杂度为$\mathcal{O}(\log n)$。  
当用图示来表示二叉堆，它非常类似于树结构，但我们仅用单个列表作为内部表示就可以实现它。二叉堆拥有两个常见的变体：最小堆(min heap)——键最小的键值拥有优先级，和最大堆(max heap)——最大的键值拥有优先级。

## 6.8 二叉堆操作 Binary Heap Operations  
二叉堆的基本操作有：  
* `BinaryHeap()` 创建一个新的空堆；
* `insert(k)` 向堆内插入新项；
* `findMin()` 返回最小键值的项，该项仍在堆内；
* `delMin()` 返回最小键值的项，从堆内删除；
* `isEmpty()` 若堆为空，返回`True`，否则`Flase`；
* `size()` 返回堆内项的数目；
* `buildHeap(list)` 从键列表中构建新的堆。  

## 6.9 二叉堆的实现 Binary Heap Implementation  
### 6.9.1 构造特性 The Structure Property  
可以利用二叉树的对数特性来表示堆，为了保证对数特性，树结构必须是平衡的——即根节点的左右子树的节点数目大致相等。在堆实现中通过构建完全二叉树来保证树平衡，由于堆的填充逐层自左至右，因此最后一层并不一定左右平衡，可以看下图所示  
![compTree.png](http://interactivepython.org/courselib/static/pythonds/_images/compTree.png)  
还有一个有趣的特性，即完全二叉树可以用一个单列表表示，无需节点引用或者列表的列表。由于其是完全填充的，左面母节点（位置p）的子节点在列表的位置2p处，于其类似，右面母节点的子节点位于位置2p+1处。列表中位置n的节点，其母结点在n/2处，下图就给出了完全树的列表表示，注意2p和2p+1的母子节点关系。因此，以上特性允许我们仅利用简单的数学操作就可以高效地遍历完全二叉树，同时它也可以高效地实现二叉堆。  
![heapOrder.png](http://interactivepython.org/courselib/static/pythonds/_images/heapOrder.png)  
### 6.9.2  堆序特性 The Heap Order Property  
堆序特性：在堆中，母结点p的任意子节点x键值都不大与母结点p的键值（最小堆）。  
### 6.9.3  堆操作 Heap Operations  
首先构建二叉堆，由于整个二叉堆可以用单列表实现，因此构建函数仅需要初始化列表并用`currentSize`来跟踪堆的当前尺寸就可以了。


```python
class BinHeap:
    def __init__(self):
        self.heapList = [0]
        self.currentSize = 0
```

可以看到空二叉堆有一个元素0作为`heapList`的第一个元素，其不被使用，但它让整除操作能够被后面的方法所使用。接下来是`insert`方法的实现，最简单有效地向列表插入项的方法是将项放到列表的末端，好的方面是保证我们保持完全二叉树的特性，但和大可能会扰乱堆的构造特性。因此，非常有必要来写一个方法，能够通过比较新插入项与其母节点来恢复堆的构造特性，如果新插入的项小于母节点的键值，就将两项交换，如下图所示：  
![percUp.png](http://interactivepython.org/courselib/static/pythonds/_images/percUp.png)  
当一个插入项向上渗透时，其实是在恢复插入项和母节点之间的堆序，同时也保持了其他兄弟节点的堆序，当然如果新插入项非常小，需要继续与更高层的节点交换，直到树的最高层。上述操作用`percUp`方法实现——将新插入项渗透到合适的层以维持堆序，这也是为何`heapList`需要一个多余元素（元素0）。而当前节点的母节点位置可以由当前节点的位置整除以2得到。  


```python
def percUp(self, i):
    while i // 2 >0:
        if self.heapList[i] < self.heapList[i // 2]:
            tmp = sef.heapList[i // 2]
            self.heapList[i // 2] = self.heapList[i]
            self.heapList[i] = tmp
        i = i // 2
```

由于`percUp`方法是将新插入项渗透到合适的层以维持堆序，因此`insert`方法的大多数工作由其完成


```python
def insert(self, k):
    self.heapList.append(k)
    self.currentSize = self.currentSize + 1
    self.percUp(self.currentSize)
```

接下来是`delMin`方法，由于最小堆的特性是根节点为最小键值，因此找到最小值项非常简单，但难点在于删除该项后如何恢复堆的结构和堆序特性。恢复堆分两步：首先，将最后一项移到根节点位置，以维持堆结构特性，但其会破坏堆序特性；然后，将该项推入到树结构中的合适位置，以恢复堆序特性，下图分步详解了根节点通过交换移动到堆中合适位置的过程。  
![percDown.png](http://interactivepython.org/courselib/static/pythonds/_images/percDown.png)  
为了维持堆序特性，需要将根节点与小于其的最小子节点交换。完成该次交换后，继续重复交换操作直到该节点位于小于其所有子节点的位置，节点向下渗透的操作由方法`percDown`和`minChild`实现。  


```python
def percDown(self, i):
    while (i*2) <= self.currentSize:
        mc = self.minChild(i)
        if self.heapList[i] > self.heapList[mc]:
            tmp = self.heapList[i]
            self.heapList[i] = self.heapList[mc]
            self.heapList[mc] = tmp
        i = mc

def minChild(self, i):
    if i*2+1 > self.currentSize:
        return i*2
    else:
        if self.heapList[i*2] < self.heapList[i*2+1]:
            return i*2
        else:
            return i*2+1
```

下面写出`delMin`操作的代码，操作的难点由附加函数`percDown`完成。


```python
def delMin(self):
    retVal = self.heapList[1]
    self.heapList[1] = self.heapList[self.currentSize]
    self.currentSize = self.currentSize - 1
    self.heapList.pop()
    self.percDown(1)
    return retVal
```

此外，还需要一个从键值列表构建整个堆的方法。给定一个键值列表，可以通过依次插入各个键值的方法构建堆，首先从拥有1项的列表开始，然后在已存列表中以$\mathcal{O}(\log n)$的操作数代价利用二分查找来合适的位置插入下一个键值，当然，在列表中间插入新的一项需要消耗$\mathcal{O}(n)$的操作数来移动列表剩下的部分以腾出空间。因此，在堆中插入n个键值总共需要消耗$\mathcal{O}(n \log n)$的操作数。当然，如果一开始就利用整个列表就可以仅消耗$\mathcal{O}(n)$的操作数来构建整个堆。


```python
def buildHeap(self, alist):
    i = len(alist) // 2
    self.currentSize = len(alist)
    self.heapList = [0] + alist[:]
    while (i > 0):
        self.percDown(i)
        i = i - 1
```

![buildheap.png](http://interactivepython.org/courselib/static/pythonds/_images/buildheap.png)  
上图显示了`buildHeap`方法如何通过交换来将初始的树[9, 6, 5, 2, 3]中的节点移动到合适位置。尽管我们从树的中间开始然后回到根部，但`percDown`方法确保最大的子节点一直会移到树的最底层。因为堆是完全二叉树，位置大于中点的任何节点都为叶节点并且没有子节点。特别注意当`i=1`时，会从根节点向下渗透，因此会需要多次交换，正如上图最右面两幅图所示，首先将9移出根节点位置，然后9又被向下移动一层，`percDown`确保能够检查接下来更深层的子节点集合以将其推到尽可能深的层。在本示例中，导致9与3的交换，现在，9已经移动到了树的最底层，再也无需交换操作了。下面给出了上图所示用树表示交换步骤的列表表示：  
i = 2  [0, 9, 5, 6, 2, 3]  
i = 1  [0, 9, 2, 6, 5, 3]  
i = 0  [0, 2, 3, 6, 5, 9]  


```python
class BinHeap:
    def __init__(self):
        self.heapList = [0]
        self.currentSize = 0


    def percUp(self,i):
        while i // 2 > 0:
          if self.heapList[i] < self.heapList[i // 2]:
             tmp = self.heapList[i // 2]
             self.heapList[i // 2] = self.heapList[i]
             self.heapList[i] = tmp
          i = i // 2

    def insert(self,k):
      self.heapList.append(k)
      self.currentSize = self.currentSize + 1
      self.percUp(self.currentSize)

    def percDown(self,i):
      while (i * 2) <= self.currentSize:
          mc = self.minChild(i)
          if self.heapList[i] > self.heapList[mc]:
              tmp = self.heapList[i]
              self.heapList[i] = self.heapList[mc]
              self.heapList[mc] = tmp
          i = mc

    def minChild(self,i):
      if i * 2 + 1 > self.currentSize:
          return i * 2
      else:
          if self.heapList[i*2] < self.heapList[i*2+1]:
              return i * 2
          else:
              return i * 2 + 1

    def delMin(self):
      retval = self.heapList[1]
      self.heapList[1] = self.heapList[self.currentSize]
      self.currentSize = self.currentSize - 1
      self.heapList.pop()
      self.percDown(1)
      return retval

    def buildHeap(self,alist):
      i = len(alist) // 2
      self.currentSize = len(alist)
      self.heapList = [0] + alist[:]
      while (i > 0):
          self.percDown(i)
          i = i - 1

bh = BinHeap()
bh.buildHeap([9,5,6,2,3])

print(bh.delMin())
print(bh.delMin())
print(bh.delMin())
print(bh.delMin())
print(bh.delMin())
```

前面所述的构建一个操作数为$\mathcal{O}(n)$的堆构建函数，而所缺少的$\log n$因子是由树的高度所衍生出来的，在大多数`buildHeap`的操作中，树的高度都小于$\log n$。

## 6.10 二叉搜索树 Binary Search Trees  
之前已经见到两种不同方式从集合中获取的键-值对，即映射抽象数据类型（map abstract data type, map ADT），这两种映射抽象数据类型分别是列表的二叉搜索和散列表。现在我们将要学习另外一种键-值的映射二叉搜索树，主要关注于用其来提供更为有效的搜索操作。  

## 6.11 搜索树操作 Search Tree Operations  
在实现搜索树之前，先回顾一下映射ADT的的接口操作，可以看到其非常像Python字典的接口：  
* `Map()`创建新的空映射；
* `put(key, val)`像映射中添加新的键-值对。如果映射中已存在该键，则用新的值取代旧的值；
* `get(key)`给出映射中对应键的值，如果没有，返回`None`；
* `del`利用声明`del map[key]`从映射中删除键-值对；
* `len()`返回映射中存取的键-值对数目；
* `in`声明`key in map`为，如果键在映射中存在返回`True`，否则返回`False`。

## 6.12 搜索树实现 Search Tree Implementation  
二叉搜索树的特性为：左子树上所有节点的值均小于它的母节点的值，右子树上所有节点的值均大于它的母节点的值，称为BST(Binary Search Tree)特性，映射接口的实现有赖于该特性。下图显示了二叉搜索树的该特性，键无对应值，所有左子树上所有节点的值均小于它的根节点的值，右子树上所有节点的值均大于它的根节点的值：  
![simpleBST.png](http://interactivepython.org/courselib/static/pythonds/_images/simpleBST.png)  
接下来我们看二叉搜索树是如何构造的。上图显示了依照70, 31, 93, 94, 14, 23, 73的顺序插入各键后的节点结构，70为第一个插入的键，位于根节点，接下来是31，小于70，为70的左子节点，然后是93大于70，是70的右子节点，现在树的两层已经被填充，再插入的节点为31或93的子节点，94大于70和93，因此其成为93的右子节点，与其类似，14小于70和31，为31的左子节点，23同样小于31，为31的左子树，但其大于14，所以成为14的右子节点。  
利用类似于链表和表达式树的节点引用方法来实现二叉搜索树。然而，由于需要创建和操作一个空的二叉搜索树，因此我们使用两个类来实现：第一个类称为`BinarySearchTree`，第二个类称为`TreeNode`。`BinarySearchTree`类有一指向`TreeNode`的引用，即二叉搜索树的根。在大多数情况下，类外定义的外部方法仅检查树是否为空。如果树中有节点，对其的要求可以传递到`BinarySearchTree`类内定义的私有方法，其将根节点作为参数。当树为空或者删除树根节点的键时，需要做一些特殊的操作。`BinarySearchTree`类构建函数以及其他一些函数如下所示：


```python
class BinarySearchTree:
    
    def __init__(self):
        self.root = None
        self.size = 0
    
    def length(self):
        return self.size
    
    def __len__(slef):
        return self.size
    
    def __iter__(self):
        return self.root.__iter__()
```

`TreeNode`类提供了许多辅助函数，以使`BinarySearchTree`类中方法的实现起来更简单。`TreeNode`的构建函数和辅助函数如下所示。这些辅助函数有助于根据节点的位置辨别其所属子类以及所拥有的子类。`TreeNode`类同时也明确追踪每个节点相对于父节点的引用。当讨论`del`操作的实现时，将明白其为何重要。  
`TreeNode`类实现的另外一个有趣的方面是使用了Python中的可变参数。可变参数有助于在几种不同的情况下创建一个`TreeNode`。有时我们想创建一个新的带有`parent`和`child`的`TreeNode`，我们可以将现有的母节点和子节点传给它作为参数。另外其他时候仅仅创建一个带有键-值对的`TreeNode`而无需传入`parent`和`child`作为参数，该情况下使用可变参数的缺省值。


```python
class TreeNode:
    def __init__(self, key, val, left=None, right=None, parent=None):
        self.key = key
        self.payload = val
        self.leftChild = left
        self.rightChild = right
        self.parent = parent
        
    def hasLeftChild(self):
        return self.leftChild
    
    def hasRightChild(self):
        return self.rightChild
    
    def isLeftChild(self):
        return self.parent and self.parent.leftChild == self
    
    def isRightChild(self):
        return self.parent and self.parent.rightChild == self
    
    def isRoot(self):
        return not self.parent
    
    def isLeaf(self):
        return not (self.rightChild or self.leftChild)
    
    def hasAnyChildren(self):
        return self.rightChild or self.leftChild
    
    def hasBothChildren(self):
        return self.rightChild and self.leftChild
    
    def replaceNodeData(self, key, value, lc, rc):
        self.key = key
        self.payload = value
        self.leftChild = lc
        self.rightChild = rc
        if self.hasLeftChild():
            self.leftChild.parent = self
        if self.hasRightChild():
            self.rightChild.parent = self
```

现在有了`BinarySearchTree`类shell和`TreeNode`，可以写`put`方法以构建二叉搜索树。`put`方法是`BinarySearchTree`类的方法，它会检查树是否已经有根节点，如果没有根节点，`put`会创建一个新的`TreeNode`并将其作为树的根节点。如果根节点已经存在，`put`会调用私有、递归辅助函数`_put`按照下面的算法搜索树：  
* 从树的根节点开始搜索二叉树，新的键与当前节点中的键比较。如果新的键小于当前节点，搜索左面子树；如果新的键大于当前节点，就搜索右面子树。  
* 当无左（或右）子树可以搜索，寻找适合的位置存放新的节点；  
* 向树添加一个节点，创建新的`TreeNode`对象并将其插入到上一步所找到的的位置。  
  
下面显示了向树中插入新节点的Python代码。`_put`函数按照上述步骤递归编写，并注意当新的子节点插入树中时，`currentNode`作为母节点传给新的树。  
但有一个问题是如果我们会对插入的重复键处理不当。因为在树的实现过程中，重复的键值会在拥有原始键节点的右子树创建一个新的相同键值的节点，结果是搜索过程中将会永远找不到带有新键值的节点。解决该问题的办法是将旧的值用新的键指向的值代替。


```python
def put(self, key, val):
    if self.root:
        self._put(key, val, self.root)
    else:
        self.root = TreeNode(key, val)
    self.size = self.size + 1
    
def _put(self, key, val, currentNode):
    if key < currentNode.key:
        if currentNode.hasLeftChild():
            self._put(key, val, currentNode.leftChild)
        else:
            currentNode.leftChild = TreeNode(key, val, parent=currentNode)
    else:
        if currentNode.hasRightChild():
            self._put(key, val, currentNode.rightChild)
        else:
            currentNode.rightChild = TreeNode(key, val, parent=currentNode)
```

随着定义完成`put`方法，便可以容易地通过添加调用`put`方法的`__setitem__`方法重载`[]`操作符，已让我们编写类似于`myZipTree['Plymouth'] = 55446`的Python声明，就像Python字典。


```python
def __setitem__(self, k, v):
    self.put(k, v)
```

下图显示了向二叉树中插入新节点的过程，灰色节点显示插入过程中访问到的节点。  
![bstput.png](http://interactivepython.org/courselib/static/pythonds/_images/bstput.png)  
接下来需要实现获取键对饮的值的方法`get`，相对与`put`方法的实现较为简单，因为其仅递归地搜索树直到到达无对应匹配的叶节点或者找到匹配的键，当找到匹配的键后，返回存储在该结点的值。  
下面的代码为`get`, `_get`以及`__getitem__`。`_get`方法中搜索的代码与`_put`方法中选择左右子树的逻辑相同。`_get`方法返回`TreeNode`给`get`，这使得`_get`成为其他的`BinarySearchTree`方法的一个灵活的辅助方法，可能需要利用`TreeNode`中除了负载以外的其他节点。  
通过编写类似于访问字典的Python声明来实现`__getitem__`，而实际上利用的是二叉搜索树，例如`z = myZipTree['Fargo']`，而且可以看到所有的`__getitem__`方法都会调用`get`。  


```python
def get(self, key):
    if self.root:
        res = self._get(key, self.root)
        if res:
            return res.payload
        else:
            return None
    else:
        return None
    
def _get(self, key, currentNode):
    if not currentNode:
        return None
    elif currentNode.key == key:
        return currentNode
    elif key < currentNode.key:
        return self._get(key, currentNode.leftChild)
    else:
        return self._get(key, currentNode.rightChild)
    
def __getitem__(self, key):
    return self.get(key)
```

利用`get`方法可以通过编写`BinarySearchTree`的`__contains__`方法来实现`in`操作。`__conrains__`方法仅调用`get`，如果`get`返回值，则返回`True`，如果`get`返回`None`，则返回`False`。


```python
def __contains__(self, key):
    if self._get(key, self.root):
        return True
    else:
        return False
```

`__contains__`重载了`in`操作符，因此允许我们写出下面的声明


```python
if 'Northfield' in myZipTree:
    print("omm ya ya")
```

最后来看二叉搜索树最具挑战性的方法，删除键。首要任务是找到要删除的节点，如果树多于一个节点，利用`_get`方法找到需要删除的`TreeNode`。如果仅有一个节点，意味着需要删除根节点，但仍需检查以确保其是否匹配要删除的键。如果上述两种情况下均未发现键，`del`操作符就会报错。


```python
def delete(self, key):
    if self.size > 1:
        nodeToRemove = self._get(key, self.root)
        if nodeToRemove:
            self.remove(nodeToRemove)
            self.size = self.size - 1
        else:
            raise KeyError('Error, key not in tree')
    elif self.size == 1 and self.root.key == key:
        self.root == None
        self.size = self.size - 1
    else:
        raise KeyError('Error, key not in tree')
        
def __delitem__(self, key):
    self.delete(key)
```

一旦发现节点含有要删除的键，有三种情况需要考虑：
1. 要删除的节点没有子节点；
2. 要删除的节点仅有一个子节点；
3. 要删除的节点有两个子节点；  
  
![bstdel1.png](http://interactivepython.org/courselib/static/pythonds/_images/bstdel1.png)  
第一种情况比较简单，如果当前节点没有子节点，仅需要将该结点删除然后把指向该结点的引用移给母节点，如下所示。


```python
if currentNode.isLeaf():
    if currentNode == currentNode.parent.leftChild:
        currentNode.parent.leftChild = None
    else:
        currentNode.parent.rightChild = None
```

第二种情况稍微复杂，如果一个节点只有一个子节点，可以提升子树代替其母结点的位置，代码如下所示，一共6种需要考虑的情况，且对于左右子节点来说相对对称，因此只需讨论左子节点就可以了：  
1. 如果当前节点是左子节点，只需更新左子节点指向母节点的引用，将母节点对左子节点的引用指向当前节点的左子节点；  
2. 如果当前节点为右子节点，只需更新右子节点指向母节点的引用，将母节点对右子节点的引用指向当前节点的左子节点；  
3. 如果当前节点没有母节点，其为根节点，只需要调用`replaceNodeDate`方法作用于根节点更换`key`, `payload`, `leftChild`和`rightChild`的数值。  
![bstdel2.png](http://interactivepython.org/courselib/static/pythonds/_images/bstdel2.png)


```python
else:
    if currentNode.hasLeftChild():
        if currentNode.isLeftChild():
            currentNode.leftChild.parent = currentNode.parent
            currentNode.parent.leftChild = currentNode.leftChild
        elif currentNode.isRightChild():
            currentNode.leftChild.parent = currentNode.parent
            currentNode.parent.rightChild = currentNode.leftChild
        else:
            currentNode.replaceNodeData(currentNode.leftChild.key, 
                                        currentNode.leftChild.payload, 
                                        currentNode.leftChild.leftChild, 
                                        currentNode.leftChild.rightChild)
    else:
    if currentNode.hasLeftChild():
        if currentNode.isLeftChild():
            currentNode.rightChild.parent = currentNode.parent
            currentNode.parent.leftChild = currentNode.rightChild
        elif currentNode.isRightChild():
            currentNode.rightChild.parent = currentNode.parent
            currentNode.parent.rightChild = currentNode.rightChild
        else:
            currentNode.replaceNodeData(currentNode.rightChild.key, 
                                        currentNode.rightChild.payload, 
                                        currentNode.rightChild.leftChild, 
                                        currentNode.rightChild.rightChild)
```

第三种情况是最难处理的情况，当一个节点拥有两个子节点，就不可能仅仅将其子节点种的一个提升到母节点的位置，这就需要搜索树来找到一个节点能够替换计划删除的节点，其能够保存二叉搜索树现有左右子树的关系，该节点称为后继元(successor)，然后是最快找到后继元的方法，后继元确保拥有不多于一个的子节点，因此可以利用已有的实现方法来移动它，去替换被删除的节点。  
![bstdel3.png](http://interactivepython.org/courselib/static/pythonds/_images/bstdel3.png)  
处理第三种情况的代码如下所示，利用了辅助函数`findSuccessor`和`findMin`来找到后继元。利用方法`splitOut`移动后继元，因为其能直接对需要分割的节点做恰当的操作，当然也可以递归地调用`delete`方法，但会在反复寻找键节点时浪费时间。  


```python
elif currentNode.hasBothChildren():
    succ = currentNode.findSuccessor()
    succ.spliceOut()
    currentNode.key = succ.key
    currentNode.payload = succ.payload
```

寻找后继元的代码如下所示，为`TreeNode`类的方法，利用了二叉搜索树中的中序遍历按从小到大打印出树节点的特性。寻找后继元有三种情况需要考虑：  
1. 如果节点拥有右子节点，后继元为右子树中的最小键；
2. 如果节点没有右子节点，并且是其母节点的左子节点，则母节点为后继元；
3. 如果节点是其母结点的右子节点，其本身并无右子节点，则该结点的后继元为其母结点，并且不包括其本身。  
调用`findMin`方法来找到子树中的最小键，而最小值一定位于二叉搜索树最左面的子节点。因此，`findMin`方法仅追寻子树每个节点的`leftChild`引用直到没有左子树的叶节点。


```python
def findSuccessor(self):
    succ = None
    if self.hasRightChild():
        succ = self.rightChild.findMin()
    else:
        if self.parent:
            if self.isLeftChild():
                succ = self.parent
            else:
                self.parent.rightChild = None
                succ = self.parent.findSuccessor()
                self.parent.rightChild = self
    return succ

def findMin(self):
    current = self
    while current.hasLeftChild():
        current = current.leftChild
    return current

def spliceOut(self):
    if self.isLeftChild():
        if self.isLeftChild():
            self.parent.leftChild = None
        else:
            self.parent.rightChild = None
    elif self.hasAnyChildren():
        if self.hasLeftChild():
            if self.isLeftChild:
                self.parent.leftChild = self.leftChild
            else:
                self.parent.rightChild = self.leftChild
            self.leftChild.parent = self.parent
        else:
            if self.isLeftChild():
                self.parent.leftChild =self.rightChild
            else:
                self.parent.rightChild = self.rightChild
            self.rightChild.parent = self.parent
```

最后来看二叉搜索树的最后一个接口方法，如何能像在字典中那样顺序地迭代树上所有的键值？利用`inorder`遍历可以顺序遍历树上所有节点，然而想要编写一个迭代还需要做一些工作，因为一个迭代器一次只返回一个节点。  
当创建迭代器时，Python提供了非常有用的函数`yield`，它类似于`return`，返回值给调用者，此外，`yield`还有额外的步骤能够冻结函数的状态，以便于下次函数调用时，继续从先前的冻点执行。创建可迭代对象的函数称为生成器。  
二叉搜索树的`inorder`遍历如下所示，乍看起来，它并不像是递归的。然而，`__iter__`重写了迭代的`for x in`操作，所以它是递归的！因为在`TreeNode`类中定义的`__iter__`是对`TreeNode`实体进行递归。


```python
def __iter__(self):
    if self:
        if self.hasLeftChild():
            for elem in self.leftChild:
                yield elem
        yield self.key
        if self.hasRightChild():
            for elem in self.rightChild:
                yield elem
```

`BinarySearchTree`和`TreeNode`类的完整代码如下：


```python
class TreeNode:
    def __init__(self, key, val, left=None, right=None, parent=None):
        self.key = key
        self.payload = val
        self.leftChild = left
        self.rightChild = right
        self.parent = parent
        
    def hasLeftChild(self):
        return self.leftChild
    
    def hasRightChild(self):
        return self.rightChild
    
    def isLeftChild(self):
        return self.parent and self.parent.leftChild == self
    
    def isRightChild(self):
        return self.parent and self.parent.rightChild == self
    
    def isRoot(self):
        return not self.parent
    
    def isLeaf(self):
        return not (self.rightChild or self.leftChild)
    
    def hasAnyChildren(self):
        return self.rightChild or self.leftChild
    
    def hasBothChildren(self):
        return self.rightChild and self.leftChild
    
    def replaceNodeData(self, key, value, lc, rc):
        self.key = key
        self.payload = value
        self.leftChild = lc
        self.rightChild = rc
        if self.hasLeftChild():
            self.leftChild.parent = self
        if self.hasRightChild():
            self.rightChild.parent = self
            
class BinarySearchTree:
    
    def __init__(self):
        self.root = None
        self.size = 0
    
    def length(self):
        return self.size
    
    def __len__(slef):
        return self.size
    
    def __iter__(self):
        return self.root.__iter__()
    
    def put(self, key, val):
        if self.root:
            self._put(key, val, self.root)
        else:
            self.root = TreeNode(key, val)
        self.size = self.size + 1

    def _put(self, key, val, currentNode):
        if key < currentNode.key:
            if currentNode.hasLeftChild():
                self._put(key, val, currentNode.leftChild)
            else:
                currentNode.leftChild = TreeNode(key, val, parent=currentNode)
        else:
            if currentNode.hasRightChild():
                self._put(key, val, currentNode.rightChild)
            else:
                currentNode.rightChild = TreeNode(key, val, parent=currentNode)
                
    def __setitem__(self, key, val):
        self.put(key, val)

    def get(self, key):
        if self.root:
            res = self._get(key, self.root)
            if res:
                return res.payload
            else:
                return None
        else:
            return None

    def _get(self, key, currentNode):
        if not currentNode:
            return None
        elif currentNode.key == key:
            return currentNode
        elif key < currentNode.key:
            return self._get(key, currentNode.leftChild)
        else:
            return self._get(key, currentNode.rightChild)

    def __getitem__(self, key):
        return self.get(key)

    def __contains__(self, key):
        if self._get(key, self.root):
            return True
        else:
            return False

    def delete(self, key):
        if self.size > 1:
            nodeToRemove = self._get(key, self.root)
            if nodeToRemove:
                self.remove(nodeToRemove)
                self.size = self.size - 1
            else:
                raise KeyError('Error, key not in tree')
        elif self.size == 1 and self.root.key == key:
            self.root == None
            self.size = self.size - 1
        else:
            raise KeyError('Error, key not in tree')

    def __delitem__(self, key):
        self.delete(key)

    def findSuccessor(self):
        succ = None
        if self.hasRightChild():
            succ = self.rightChild.findMin()
        else:
            if self.parent:
                if self.isLeftChild():
                    succ = self.parent
                else:
                    self.parent.rightChild = None
                    succ = self.parent.findSuccessor()
                    self.parent.rightChild = self
        return succ

    def findMin(self):
        current = self
        while current.hasLeftChild():
            current = current.leftChild
        return current

    def spliceOut(self):
        if self.isLeftChild():
            if self.isLeftChild():
                self.parent.leftChild = None
            else:
                self.parent.rightChild = None
        elif self.hasAnyChildren():
            if self.hasLeftChild():
                if self.isLeftChild:
                    self.parent.leftChild = self.leftChild
                else:
                    self.parent.rightChild = self.leftChild
                self.leftChild.parent = self.parent
            else:
                if self.isLeftChild():
                    self.parent.leftChild =self.rightChild
                else:
                    self.parent.rightChild = self.rightChild
                self.rightChild.parent = self.parent
            
    def remove(self, currentNode):
        # leaf
        if currentNode.isLeaf():
            if currentNode == currentNode.parent.leftChild:
                currentNode.parent.leftChild = None
            else:
                currentNode.parent.rightChild = None
        # interior
        elif currentNode.hasBothChildren():
            succ = currentNode.findSuccessor()
            succ.spliceOut()
            currentNode.key = succ.key
            currentNode.payload = succ.payload
        # this node has one child      
        else:
            if currentNode.hasLeftChild():
                if currentNode.isLeftChild():
                    currentNode.leftChild.parent = currentNode.parent
                    currentNode.parent.leftChild = currentNode.leftChild
                elif currentNode.isRightChild():
                    currentNode.leftChild.parent = currentNode.parent
                    currentNode.parent.rightChild = currentNode.leftChild
                else:
                    currentNode.replaceNodeData(currentNode.leftChild.key, 
                                                currentNode.leftChild.payload, 
                                                currentNode.leftChild.leftChild, 
                                                currentNode.leftChild.rightChild)
            else:
                if currentNode.hasLeftChild():
                    if currentNode.isLeftChild():
                        currentNode.rightChild.parent = currentNode.parent
                        currentNode.parent.leftChild = currentNode.rightChild
                    elif currentNode.isRightChild():
                        currentNode.rightChild.parent = currentNode.parent
                        currentNode.parent.rightChild = currentNode.rightChild
                    else:
                        currentNode.replaceNodeData(currentNode.rightChild.key, 
                                                    currentNode.rightChild.payload, 
                                                    currentNode.rightChild.leftChild, 
                                                    currentNode.rightChild.rightChild)
```


```python
mytree = BinarySearchTree()
mytree[3] = "red"
mytree[4] = "blue"
mytree[6] = "yellow"
mytree[2] = "at"
```


```python
mytree[6]
```




    'yellow'




```python
mytree[2]
```




    'at'



## 6.13 搜索树分析 Search Tree Analysis  
下面来分析二叉搜索树的实现的方法。首先是`put`方法，限制它执行效率的因素是树的高度，高度作为一种限制因素是因为当我们在树中寻找一个插入节点的合适位置时，需要在每一级至多进行一次比较。  
树的高度取决于键添加的方式，如果键是随机添加到树中，则当有n个节点树高为$\log_{2} n$，因为如果树是随机散布，大约一半的节点会大于根节点，一半会小于。在二叉搜索树中，根节点有1个，之下一层有2个节点，再之下有4个节点，第d层拥有的节点数为$2^d$。高度为h的二叉搜索树拥有节点$2^{h+1}-1$个。  
完美平衡的二叉搜索树左右子树拥有的节点数目相等。在拥有n个节点的平衡二叉树中，`put`的执行效率为$\mathcal{O}(\log_2 n)$，与之前所述为逆运算。因此$\log_{2} n$给出了树高，代表了把一个新节点插入一个合适位置所需要做的 put 的最多次数。  
不幸的是，通过插入排序好了的键，建造一个高度为 n 的搜索树是可能的。下图就展示了这种树的一个例子，在这个情形下，这个 `put` 方法的执行复杂度为 $\mathcal{O}(n)$。  
![skewedTree.png](http://interactivepython.org/courselib/static/pythonds/_images/skewedTree.png)  
同样`get`, `in`, `del`也受限于树的高度。为通过 `get` 搜索树来发现键，在最坏的情形下，要一直搜索树到底而未找到键。乍一看 `del` 看上去也许更复杂，因为它可能需要在删除操作完成之前一直查找下一个后继元节点。但寻找后继元节点的最坏情形也只是树的高度，即只需要简单地把工作加倍，因为加倍是乘以一个常数因子，所以它没有改变最坏的情形（时间复杂度）。


```python

```
