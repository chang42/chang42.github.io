
# 排序和搜索 Sorting and Searching  
## 5.1 搜索 Searching  
搜索（Searching）是在项的集合中寻找特定项的算法程序。搜索返回的结果为布尔值 `True` 或 `False` 代表所寻找的项是否存在，当然它也可以返回项所在的位置。  
在Python中，利用 `in` 操作可以非常简单地搜索项是否位于集合内：


```python
8 in [1, 2, 3, 4, 5]
```




    False




```python
3 in [1, 2, 3, 4, 5]
```




    True



实现搜索有很多方法，我们更加关注于算法的实现和性能。  
## 5.2 顺序搜索 The Sequential Search  
当数据项排序在诸如列表等集合中，我们称其为线性或顺序关系。每一个数据项排序在相对位置，在Python列表中，索引代表其相对位置，非常便于我们顺序访问，该操作即为顺序搜索（Sequential Search）。  
![seqsearch.png](http://interactivepython.org/courselib/static/pythonds/_images/seqsearch.png)  
上图所示为顺序（线性）搜索，从列表第一项开始，依次搜索直到找到所要寻找的项，如果走出列表则表明所要寻找的项不存在。该算法的Python表示如下所示，参数为所搜寻的列表和目标项，返回布尔值 `True` 或者 `False` 。  


```python
def sequentialSearch(alist, item):
    pos = 0
    found = False
    
    while pos < len(alist) and not found:
        if alist[pos] == item:
            found = True
        else:
            pos = pos+1
    return found
```


```python
testlist = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
```


```python
sequentialSearch(testlist, 0)
```




    True




```python
sequentialSearch(testlist, 10)
```




    False



在搜索算法中，比较是重复最多的操作，并且因为列表是无序的，所需搜寻的项可以位于列表的任意位置，等价于搜索可以从列表的任意位置开始。如果所要搜寻的项不在列表中，就需要比较完列表中的所有项，也有可能所要搜寻的项位于列表的起首位置，平均下来需要比较$\frac{n}{2}$项，所以算法的复杂度为$\mathcal{O}(n)$。  
  
| |最好情况|最坏情况|平均|
|:-:|:-:|:-:|:-:|
|项在列表中|1|n|n/2|
|项不在列表中|n|n|n|  
  
如果列表是有序的呢？因为所要搜寻的项可以位于列表的任意位置，所以该情况下，算法的复杂度仍然为$\mathcal{O}(n)$。但如果所需搜寻的项不在列表中，情况会稍有不同，如下面的图中所示，所需搜寻的项为50，当比较完项54时，我们直到其后任意一项都比它大，所以程序就不用继续往下比较了。  
![seqsearch2.png](http://interactivepython.org/courselib/static/pythonds/_images/seqsearch2.png)  


```python
def orderedSequentialSearch(alist, item):
    pos = 0
    found = False
    stop = False
    while pos < len(alist) and not found and not stop:
        if alist[pos] == item:
            found = True
        elif alist[pos] > item:
            stop = True
        else:
            pos = pos + 1
    return found
```


```python
testlist = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
```


```python
orderedSequentialSearch(testlist, 0)
```




    False




```python
orderedSequentialSearch(testlist, 5.5)
```




    False



| |最好情况|最坏情况|平均|
|:-:|:-:|:-:|:-:|
|项在列表中|1|n|n/2|
|项不在列表中|1|n|n/2|  
  
## 5.3 二分查找 The Binary Search  
利用上面的顺序查找在有序列表中搜索特定项，比较完第一项之后，没有找到，接下来继续比较n-1项，但是如果用二分查找从比较中间一项开始，如果是所要查找的项，完成搜索，如果没有找到，且所要查找的项大于中间项，删掉中间项连带列表的下半部分，反之，删掉中间项和列表的上半部分，再做查找，重复以上步骤，直到完成查找。  
![binsearch.png](http://interactivepython.org/courselib/static/pythonds/_images/binsearch.png)


```python
def binarySearch(alist, item):
    first = 0
    last = len(alist) - 1
    found = False
    
    while first <= last and not found:
        midPoint = (first + last) // 2
        if alist[midPoint] == item:
            found = True
        elif alist[midPoint] > item:
            last = midPoint - 1
        else:
            first = midPoint + 1
    
    return found
```


```python
testlist = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
```


```python
binarySearch(testlist, 3)
```


```python
binarySearch(testlist, 13)
```

分析上面的算法，其采用了分而治之（divide and conquer）的策略，即将一个复杂问题分割为小的部分，先解决小的部分，再重新组合整个问题得出结果。通过上面的描述，我们发现这也是一个递归函数，所以：


```python
def binarySearch(alist, item):
    if len(alist) == 0:
        return False
    else:
        midPoint = len(alist) // 2
        if alist[midPoint] == item:
            return True
        elif alist[midPoint] > item:
            return binarySearch(alist[:midPoint], item)
        else:
            return binarySearch(alist[midPoint+1:], item)
```


```python
testlist = [1, 2, 3, 4, 5, 6, 7, 8, 9, 0]
```


```python
binarySearch(testlist, 3)
```


```python
binarySearch(testlist, 13)
```

如果开始有n项，第一次比较后，会去掉一半留下n/2项，第二次会留下n/4项，第三次会留下n/8项，以此类推：  
  
|比较|剩余项的数目|
|:-:|:-:|
|1|n/2|
|2|n/4|
|3|n/8|
|...|...|
|i|n/2^i|  
  
当分割足够多的次数，列表中就会留下一项，再比较返回结果完成查找，此即寻找i使$\frac{n}{2^i}=1$，得到$i=\log n$，最多需要比较的次数为列表项数的对数，因此，其复杂度为$\mathcal{O}(\log n)$，需要注意的是在程序的递归调用中我们利用了列表的切片 `binarySearch(alist[:midpoint],item)` ，来产生列表的左（下）半部分传递到下一次调用中，在Python中切片操作的复杂度为$\mathcal{O}(k)$，所以实际上二分查找的性能并不能达到列表项数的对数，但我们可以先计算切片部分的开始和结束的索引，然后再进行切片。  
虽然二分查找通常优于顺序查找，但是对于小的列表长度n并不值得额外的耗费来排序。实际上，我们经常需要考虑排序的额外耗费来获取查找的优势，如果我们排序一次，多次查找，就非常值得牺牲额外的耗费来做排序，当然，对于一个大列表，即使一次排序的耗费就非常大，这样从头开始查找则会是一个相对不错的选择。  
## 5.4 散列/哈希 Hashing  
下面，我们更进一步来构建一种数据结构，使搜索的复杂度为$\mathcal{O}(1)$，即散列法。它的基本思想是将列表中的项压缩成摘要，使得数据量变小，便于查找，散列表中的每一个位置称为插槽（slot）。例如下图所示，有一个长度为11的散列表，插槽名分别为0，1，2, ...， 10，项与插槽之间的映射关系为散列函数，散列函数将集合中的项映射到0到10的插槽名上。  
![hashtable.png](http://interactivepython.org/courselib/static/pythonds/_images/hashtable.png)  
假设有54，26，93，17，77和31，可以用取余方法作为散列函数，各项除以列表的长度11，余数作为散列值$(h(item)=item%11)$。  
  
|项|散列值|
|:-:|:-:|
|54|10|
|26|4|
|93|5|
|17|6|
|77|0|
|31|9|
  
项被插入散列值对应的位置，11个插槽的6个位置被占用，装载因子（load factor）为$\lambda = \frac{numberofitemd}{tablesize}=\frac{6}{11}$。  
![hashtable2.png](http://interactivepython.org/courselib/static/pythonds/_images/hashtable2.png)  
如果想要查找某项，利用散列函数计算出插槽名，查看其是否存在于散列表，该查找操作复杂度为$\mathcal{O}(1)$，因为计算散列值并索引列表的对应位置为常数计算量。但现在还面临一个问题，即如果有一项为44那么取余为0，与77位于同一个插槽，该情况称为冲突（collision/clash）。  
### 5.4.1 散列函数 Hash Functions  
如果散列函数能将各项映射到各自独立的插槽中，其为理想散列函数。但对于随机给定的项集合，并没有一个系统的方法构建理想散列函数，但一个不那么理想的散列函数已经非常有效了。  
构建理想散列函数的一个办法是增加散列表的长度使其能容纳每一项，这保证了每一项都有一个特定的插槽，但对于大数字的项会遇到困难，例如我们项存下25个学生的15位身份证号，就会浪费掉很多资源。  
更为理想的散列函数应该尽可能减小冲突的可能、易于计算且使散列表均匀分布。折叠法（folding method）即将关键字分割成位数相同的几部分（最后一部分的位数可以不同），然后取这几部分的叠加和（舍去进位）作为散列值。例如记录10位电话号码436-555-4601，可以将其分为两位数组成的数字组（43, 65, 55, 46, 01），然后相加43+65+55+46+01=210，如果散列表有11个插槽，那么再除11取余210%11=1，或者再反转某一个值43+56+55+64+01=219，再11取余219%11=1。  
另外还有一种平方取中法（mid-square method），取关键字平方后的中间几位为散列值，例如项44平方后$44^2=1936$，取中间两位93，除11取余得到5，下表为利用平方取中法得到各项的散列值。  
  
|Item|Remainder|Mid-Square|
|:-:|:-:|:-:|
|54|10|3|
|26|4|7|
|93|5|9|
|17|6|8|
|77|0|4|
|31|9|6|
  
同样可以对字符串中的字母创建散列函数，字母被视为一系列有序的值,例如单词“cat”。


```python
ord('c')
```




    99




```python
ord('a')
```




    97




```python
ord('t')
```




    116



然后利用有序值相加利用取余法得到单词的散列值：  
![stringhash.png](http://interactivepython.org/courselib/static/pythonds/_images/stringhash.png)  
函数 `hash` 输入字符串返回0 到 `tableSize` -1 之间的散列值。


```python
def hash(aString, tablSize):
    sum = 0
    for pos in range(len(aString)):
        sum = sum + ord(aString[pos])
    
    return sum%tableSize
```

考虑到颠倒次序的单词得到和散列值与原单词相同，再以每个字母的位置当作权重相乘:  
![stringhash2.png](http://interactivepython.org/courselib/static/pythonds/_images/stringhash2.png)  
需要注意的是散列函数不要过于复杂，这样就会舍本逐末，将计算过多的耗费在计算散列值上了。  
### 5.4.2 处理冲突CollisionResolution  
散列不发生冲突的可能性非常之小，必须有一系统的方法来在散列表放置冲突项，所以通常对冲突进行处理（CollisionResolution）。办法之一是在散列表中寻找另外一个开放的插槽来放置冲突项，比如从其应在在散列表的插槽位置开始向后依次探测，直到遇到第一个空插槽，这种尝试寻址下一个空插槽的方法称为开放定址法（openaddressing），而上述依次访问每一个插槽的方法为线性探测(LinearProbing)，在维基百科上的定义为：  
>开放定址法（openaddressing）：$hash_i=(hash(key)+d_i)\ mod\ m, i=1,2...k(k\le m-1)$，其中$hash(key)$为散列函数，$m$为散列表长，$d_i$为增量序列，$i$为已发生冲突的次数。增量序列可有下列取法：  
$d_i=1,2,3...(m−1)$称为线性探测(Linear Probing)；即$d_i=i$，或者为其他线性函数。相当于逐个探测存放地址的表，直到查找到一个空单元，把散列地址存放在该空单元。  
$d_i=±1^2,±2^2,±3^2...±k^2(k\le m/2)$称为平方探测(Quadratic Probing)。相对线性探测，相当于发生冲突时探测间隔$d_i=i62$个单元的位置是否为空，如果为空，将地址存放进去。  
$d_i=伪随机数序列$，称为伪随机探测(Pseudorandom Probing)  
  
对于整数序列(54,26,93,17,77,31,44,55,20)，当44放到插槽0时，发生冲突，线性探测会依次寻找空插槽，当发现插槽1为空时，将44放进去。然后是55，放到插槽2中，再然后是20访问插槽10，0，1，2最后放到插槽3。  
![hashtable2.png](http://interactivepython.org/courselib/static/pythonds/_images/hashtable2.png)
![linearprobing1.png](http://interactivepython.org/courselib/static/pythonds/_images/linearprobing1.png)  
用开放定址和线性探测法生成的散列表，在查找时也应遵循该法则，例如查找93，根据散列值5寻找插槽5，里面为93返回 `True` ，对于20，散列值9对应的值为31，然后需要在该插槽之后依次查找，直到找到20，返回 `True` 或者第一个空插槽，返回 `False` 。  
但线性探测的弊端是会产生聚集（Cluster），在函数地址的表中，散列函数的结果不均匀地占据表的单元，在发生冲突的位置周围形成区块。会对其他插入项有影响，例如添加项20时，在散列值0处的聚集使它跳过这些插槽，在之后寻找空插槽。  
![clustering.png](http://interactivepython.org/courselib/static/pythonds/_images/clustering.png)  
可以通过“+3”探测法一定程度上避免聚集，以上方法通称为再散列（rehashing），对于简单的线性探测：  
$$newhashvalue=rehash(oldhashvalue),rehash(pos)=(pos+1)%sizeoftable$$  
![linearprobing2.png](http://interactivepython.org/courselib/static/pythonds/_images/linearprobing2.png)  
对于“+skip”探测：  
$$newhashvalue=rehash(oldhashvalue),rehash(pos)=(pos+skip)%sizeoftable$$   
为了保证所有的插槽都能被寻址，通常选用散列表的长度作为 skip 值。  
此外还有平方探测(Quadratic Probing)  
![quadratic.png](http://interactivepython.org/courselib/static/pythonds/_images/quadratic.png)  
此外，另外一个办法是链接（Chaining），将冲突项放到同一个散列值下，当项增多时，会增加搜索的难度。当我们需要搜索项时，找到对应的散列值位置，在该散列值位置下的集合中寻找该项是否存在，这看起来似乎会使搜索更有效，但是实际并不一定。  
![chaining.png](http://interactivepython.org/courselib/static/pythonds/_images/chaining.png)    
### 5.4.3 映射数据结构的表示 Implementing the Map Abstract Data Type  
Python中的字典有着键-值的结构，键用来搜索对应值，此即为映射（map）。映射数据类型的结构为键与值之间联系的无序集合，键-值之间的映射唯一，映射的操作有：  
* `map()` 创建一个新的空映射，返回一个空映射集合。  
* `put(key, val)` 在映射中添加新的键-值对，如果键已经存在，替换掉旧的值。  
* `get(key)` 给出一个键，返回保存于映射中的值，否则返回 `None` 。  
* `del` 在映射中删除键值对，语法为 `del map[key]` 。  
* `len()` 返回映射中键值对的数目。  
* `in` 返回 `Ture` 如果键位于映射中，语法为 `key in map` ，否则返回 `False` 。  
  
字典的一个优势是给定键，迅速返回对应的值，利用上述查找复杂度为$\mathcal{O}(1)$的散列表可以实现如此快速的查找。在下面的代码块中，利用两个列表创建 `HashTable` 类表示映射抽象数据类型，两个列表分别为 `slots` 和 `data` ，分别保存键和值。


```python
class HashTable:
    def __init__(self):
        self.size = 11
        self.slots = [None] * self.size
        self.data = [None] * self.size
```

`hashfunction` 表示简单的取余方法，冲突问题的解决方法为利用“+1”再散列函数的线性探测， `put` 函数假设 `self.slots` 为空，计算出初始散列值，如果对应的插槽不为空，循环利用 `rehash` 函数找到空插槽。如果没有空插槽，替换掉旧的值。


```python
def put(self, key, data):
    hashValue = self.hashFunction(key, len(self.slots))
    
    if self.slots[hashValue] == None:
        self.slots[hashValue] = key
        self.data[hashValue] = data
    else:
        if self.slots[hashValue] == key:
            self.data[hashValue] = data
        else:
            nextSlot = self.rehash(hashValue, len(self.slots))
            while self.slots[nextSlot] != None and self.slots[nextSlot] != key:
                nextSlot = self.rehash(nextSlot, len(self.slots))
                
            if self.slots[nextSlot] == None:
                self.slots[nextSlot] = key
                self.data[nextSlot] = data
            else:
                self.data[nextSlot] = data

def hashFunction(self, key, size):
    return key % size

def rehash(self, oldHash, size):
    return (oldHash + 1) % size
```

此外，`get` 函数计算初始散列值，如果该散列值不在初始插槽，用 `rehash` 函数定位下一个可能的位置。最后的 `__getitem__` 和 `__setitem__` 方法允许利用“[]”关联。


```python
def get(self, key):
    startSlot = self.hashFunction(key, len(self.slots))
    
    data = None
    stop = False
    found = False
    position = startSlot
    while self.slots[position] != None and not found and not stop:
        if self.slots[position] == key:
            found = True
            data = self.data[position]
        else:
            position = self.rehash(position, len(self.slots))
            if position == startSlot:
                stop = True
    return data

def __getitem__(self, key):
    return self.get(key)

def __setitem__(self, key, data):
    self.put(key, data)
```

创建一个 `HashTable` 类的例子：


```python
class HashTable:
    def __init__(self):
        self.size = 11
        self.slots = [None] * self.size
        self.data = [None] * self.size
        
    def put(self, key, data):
        hashValue = self.hashFunction(key, len(self.slots))

        if self.slots[hashValue] == None:
            self.slots[hashValue] = key
            self.data[hashValue] = data
        else:
            if self.slots[hashValue] == key:
                self.data[hashValue] = data
            else:
                nextSlot = self.rehash(hashValue, len(self.slots))
                while self.slots[nextSlot] != None and self.slots[nextSlot] != key:
                    nextSlot = self.rehash(nextSlot, len(self.slots))

                if self.slots[nextSlot] == None:
                    self.slots[nextSlot] = key
                    self.data[nextSlot] = data
                else:
                    self.data[nextSlot] = data

    def hashFunction(self, key, size):
        return key % size

    def rehash(self, oldHash, size):
        return (oldHash + 1) % size
    
    def get(self, key):
        startSlot = self.hashFunction(key, len(self.slots))

        data = None
        stop = False
        found = False
        position = startSlot
        while self.slots[position] != None and not found and not stop:
            if self.slots[position] == key:
                found = True
                data = self.data[position]
            else:
                position = self.rehash(position, len(self.slots))
                if position == startSlot:
                    stop = True
        return data

    def __getitem__(self, key):
        return self.get(key)

    def __setitem__(self, key, data):
        self.put(key, data)
```


```python
H = HashTable()
```


```python
H[54] = "cat"
```


```python
H[26] = "dog"
```


```python
H[93] = "lion"
```


```python
H[17] = "tiger"
```


```python
H[77] = "bird"
```


```python
H[31] = "cow"
```


```python
H[44] = "goat"
```


```python
H[55] = "pig"
```


```python
H[20] = "chicken"
```


```python
H.slots
```




    [77, 44, 55, 20, 26, 93, 17, None, None, 31, 54]




```python
H.data
```




    ['bird',
     'goat',
     'pig',
     'chicken',
     'dog',
     'lion',
     'tiger',
     None,
     None,
     'cow',
     'cat']




```python
H[20]
```




    'chicken'




```python
H[17]
```




    'tiger'




```python
H[20] = 'duck'
```


```python
H[20]
```




    'duck'




```python
H.data
```




    ['bird',
     'goat',
     'pig',
     'duck',
     'dog',
     'lion',
     'tiger',
     None,
     None,
     'cow',
     'cat']




```python
print(H[99])
```

    None


### 5.4.4 散列表分析 Analysis of Hashing  
考虑装载因子 $\lambda$ ，$\lambda$很小的话，冲突发生的可能就会很小，即项更大概率地位于它应该在的位置；如果$\lambda$很大，意味着散列表被添充满，冲突的可能性很大，也意味着冲突的解决非常困难，需要更多的比较来发现空插槽。利用链接，冲突的增加，意味着每一个链接下的项数增多。  
对于每一次成功或不成功的查找，其所需要的比较次数分别为 $\frac{1}{2}(1+\frac{1}{1-\lambda})$ 和 $\frac{1}{2}(1+(\frac{1}{1-\lambda})^2)$ ，如果利用链接，平均的比较次数为成功 $1+\lambda$，不成功$\lambda$。  
## 5.5 排序 Sorting  
排序即将集合内的元素按照一定的顺序排列。排序是计算机科学的一个重要研究方向，排序大量元素需要消耗巨量的计算资源，因此，需要找到一些改进的方法。在比较各算法的优略之前，我们需要先选定一个标准，首先，排序一个列表需要比较两个元素的大小，因此，比较次数是排序通用的衡量标准，此外，当元素未在正确的位置，需要与其他元素交换位置，交换的次数也是衡量排序算法标准。  
## 5.6 冒泡排序 The Bubble Sort    
冒泡排序多次遍历列表，它比较相邻项并交换错序的项，每一次遍历都将更大的项放到合适的位置，实际上，每个项“冒泡”到所属位置。  
![bubblepass.png](http://interactivepython.org/courselib/static/pythonds/_images/bubblepass.png)  
上图显示了冒泡排序的第一次遍历，阴影两项做对比，如果列表有n项，一次遍历需要n-1次对比。一旦最大项位于比较对中，就会一直沉淀直到完成该次遍历。当第二次遍历开始时，无序项为n-1个，需要n-2次对比，直到n-1次遍历，最小项位于正确的位置。  


```python
def bubbleSort(alist):
    for passNum in range(len(alist)-1, 0, -1):
        for i in range(passNum):
            if alist[i] > alist[i+1]:
                temp = alist[i]
                alist[i] = alist[i+1]
                alist[i+1] = temp
```


```python
alist = [2, 5, 1, 3, 6, 9, 8, 7, 0, 4]
```


```python
bubbleSort(alist)
```


```python
alist
```




    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]



交换操作称为“swap”，在Python中的表示与其他语言略有不同。通常交换列表中的两项需要额外的缓存：  
```
temp = alist[i]
alist[i] = alist[j]
alist[j] = temp
```  
上面的片段会交换列表中的第i项和第j项，如果没有临时缓存，其中一个值就会被覆盖。但在Python中，可以通过一次同时赋值声明 `a, b = b, a` 来实现交换操作。  
![](http://interactivepython.org/courselib/static/pythonds/_images/swap.png)  
无论列表中n个元素如何排列，冒泡排序都需要经历n-1次遍历重新排列，列表中显示了每一次遍历的比较次数，一次冒泡排序总共比较次数为$\frac{1}{2}n^2-\frac{1}{2}n$次，复杂度为$\mathcal{O}(n^2)$。最理想的情况下，一次交换都不需要，最差是每次比较都需要交换，平均为比较次数的一半。  
  
|遍历|比较|
|:-:|:-:|
|1|n-1|
|2|n-2|
|3|n-3|
|...|...|
|n-1|1|
  
如果排序遍历完一次后，不需要交换，那么列表肯定是有序的，我们就可以提前结束排序程序，这也是冒泡排序的一个优势，相应代码如下：


```python
def shortBubbleSort(alist):
    exchanges = True
    passNum = len(alist) - 1
    while passNum > 0 and exchanges:
        exchanges = False
        for i in range(passNum):
            if alist[i] > alist[i+1]:
                exchanges = True
                temp = alist[i]
                alist[i] = alist[i+1]
                alist[i+1] = temp
        passNum = passNum - 1
```


```python
alist = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
```


```python
shortBubbleSort(alist)
```


```python
alist
```




    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]



动图显示冒泡排序


```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation
from matplotlib import rc

# equivalent to rcParams['animation.html'] = 'html5'
rc('animation', html='html5')

fig = plt.figure()
plt.title('Bubble Sort')

alist = [2, 5, 1, 3, 6, 9, 8, 7, 4]

color = ['gray']*len(alist)
ims = []

for passNum in range(len(alist)-1, 0, -1):
    for i in range(passNum):
        color[i] = 'red'
        color[i+1] = 'red'
        im1 = plt.bar(np.arange(len(alist)), alist, color=color, animated=True, visible=True)
        plt.xticks([])
        plt.yticks([])
        ims.append(im1)
        if alist[i] > alist[i+1]:
            temp = alist[i]
            alist[i] = alist[i+1]
            alist[i+1] = temp
        im2 = plt.bar(np.arange(len(alist)), alist, color=color, animated=True, visible=True)
        plt.xticks([])
        plt.yticks([])
        ims.append(im2)
        color[i] = 'gray'
        color[i+1] = 'gray'
        
ani = animation.ArtistAnimation(fig, ims, interval=50, blit=True, repeat_delay=1000)
ani
```




<video width="432" height="288" controls autoplay loop>
  <source type="video/mp4" src="data:video/mp4;base64,AAAAHGZ0eXBNNFYgAAACAGlzb21pc28yYXZjMQAAAAhmcmVlAAA2Y21kYXQAAAKuBgX//6rcRem9
5tlIt5Ys2CDZI+7veDI2NCAtIGNvcmUgMTQ4IHIyNjQzIDVjNjU3MDQgLSBILjI2NC9NUEVHLTQg
QVZDIGNvZGVjIC0gQ29weWxlZnQgMjAwMy0yMDE1IC0gaHR0cDovL3d3dy52aWRlb2xhbi5vcmcv
eDI2NC5odG1sIC0gb3B0aW9uczogY2FiYWM9MSByZWY9MyBkZWJsb2NrPTE6MDowIGFuYWx5c2U9
MHgzOjB4MTEzIG1lPWhleCBzdWJtZT03IHBzeT0xIHBzeV9yZD0xLjAwOjAuMDAgbWl4ZWRfcmVm
PTEgbWVfcmFuZ2U9MTYgY2hyb21hX21lPTEgdHJlbGxpcz0xIDh4OGRjdD0xIGNxbT0wIGRlYWR6
b25lPTIxLDExIGZhc3RfcHNraXA9MSBjaHJvbWFfcXBfb2Zmc2V0PS0yIHRocmVhZHM9MSBsb29r
YWhlYWRfdGhyZWFkcz0xIHNsaWNlZF90aHJlYWRzPTAgbnI9MCBkZWNpbWF0ZT0xIGludGVybGFj
ZWQ9MCBibHVyYXlfY29tcGF0PTAgY29uc3RyYWluZWRfaW50cmE9MCBiZnJhbWVzPTMgYl9weXJh
bWlkPTIgYl9hZGFwdD0xIGJfYmlhcz0wIGRpcmVjdD0xIHdlaWdodGI9MSBvcGVuX2dvcD0wIHdl
aWdodHA9MiBrZXlpbnQ9MjUwIGtleWludF9taW49MjAgc2NlbmVjdXQ9NDAgaW50cmFfcmVmcmVz
aD0wIHJjX2xvb2thaGVhZD00MCByYz1jcmYgbWJ0cmVlPTEgY3JmPTIzLjAgcWNvbXA9MC42MCBx
cG1pbj0wIHFwbWF4PTY5IHFwc3RlcD00IGlwX3JhdGlvPTEuNDAgYXE9MToxLjAwAIAAAASZZYiE
AD///vdonwKbWkN6gOSVxSXbT4H/q2dwfI/pAwAAAwAArqxz6KZIGG35/EeQa4AGz3akCxG4j6ju
h8ouHGWEK82/X/6fPWeJQXUZpq94pnZLBfSKtr4oGMfWw8OrzLnQwHQMW9cxm+mMmS1pYFIh+W80
s5Ds0JjMUEATMFHk19DdZ0y46dtIJRHiNCNeifiloQLscbmwjjqWdnoybQ4QxuOCpvC6mlED6vRu
iey68eETZEs21YIN/1AutKV49Xo8cjrBnY92Qo/edEvwkkBnck/CGta0KDVUOi6mgoAwQ0aQFld/
OZbjvrsVeiieu+VbfNHw/pikEu6WfDZaJc9RxEi6TqCnZ2aLULKqeD7yfgTHuC5GiUjZjGY+U0fW
Dt6e5L6dMRW4SjEA4iFAhfNnI0GKElTyoQbmG14VakIJdVR/NJagtHAoRUh8Ltiy2kP4HrOy2EJ0
p7KjuHwCvtBWU81mG7Ah2HqtgeFV0Y4bIhbsYT/y5YPOwsYs59s8WaNotM7IJAWrQDH7B61Jh1hI
9aOhbg26IP0WMmDysZSQ12MiTAWDkB3ulhTrN5hsUV/bGV4z2Imi91l+fuJPLB+RJO3z4+eaZZ5a
GjTRbicCr8Eri70NCx8uRzoBzu9mOH9zFj3Jm77iADIE4KmTNF8AgoVTQ6/NdJstrMFG418drEii
SpSoeuOITR7fBb2jALH9WJxxBEaHe9ah+75YbUy2bHE8GlAYSQA4ytmlvn7a1d7SzTFcsfIBPtOa
Ptl0wmJ+zgoowtK2vJzSRgLeo/cSugj6AbDk7OqU7UZKF62CiUzs/yJOTUn6mOK6O2kmt5iD07i8
g8L0xZNjlq3JkhgADks62b2/37I+A+H4JNGo06Z1BachBR0wh2LUZ7CVV6A++/lXArg/hE2FjNWA
J7v2UJsc96Zqp00u4HzX6eIHOS+V0h/AzqcQPTKNQNhGdnf/wtUMd6ODT2T3qTlQKRrfFyq2DgT4
IwmWSQy/YrgDhuFgEINSdriXpZMLuc7EPfh9Spltj4ogxqf0TW/Wz2bdz66Qw2ipxpHpNtpbXVkG
IsKe5yG1UcbNGNAO1Lu9cJY3yVzoHj3yMC1qhZHZp2mVMTV+dwwH9GAcxZLm0UrKWtbbriFFQpk8
tA0E4N6fTZl7f9AjhD2vMTM0nf0WPio9xeXN9U1iclVcp23/2nbkuATftlxct3MbMotULeh/DGX0
9d8XuYzDnqsLfYHrIXtvucrbId/+JTbcetxWjeqpuDqPrcH5Z3FJAAnvRNoph+ADT0XFHAXvMoWv
X713W65iSKtWuKfEANA+hp4dTJHNRlndKKF9oMZIOQuTCCSLtr6w8xf+EquyQV5+AnPDGqJ54JXi
WrPMc2GM86qwXyYC+HxsQJ2laLEmIrxO7UAHeWmdRkeQKYn4KkBn4O8YZisBdzfsT6f1lgx3PVBm
XmtCVl9kYXKxfzlKV+BGYjPl0GIPWUSlI9XOk0WjwBKctEWCh+Hf4sX+xD1znhklBr0qikqI62GO
tUjRaYSPeULRhlrzbPi3M3+VRTBMauS1AAAYRWqIawAgoQAAAmFBmiRsQ//+qZYFIPLwCEasOeAk
cOD+NnoEOMpTPrPHMFWAA9M50Z5GnVxLxuHPF5sumJqTbXkS3rx1HgKIVx83sO+/Ve7IjBZqBc5v
ZuMKMtqoSumSnzQ4SJLZsXU7k+tM16Wx4yglVP/w60VdjF/G8A8ncxCmM/VPdZTTE130LL7bbaBG
c2qdJWPNCIuclFnuhp9ahRxeNNDqEkUm+on1fyNDUzb4r8iS16DKuaAUxWrDRkddt8Z9ZfxniQdJ
aTa7dnoOJeoXIDmjplWkYs+XL3W60a4CE1AjjybQYxkIXVhrBQQG3vm/z+6lviAOa2E/aREp8WyD
uPq12A/fuILFzeipmklhi1PdjjwAHDusuz2UnOmxlKwTvTMY+9h5SwGexegmEf8tWsXZjz0WFsvw
zHRbO43dku220uDV7ySPGLHcwCirvVO6m5o0W89p/BymshGjXETApsoUSHY0Vo2ESLajNmlwbt7d
k5vBKrBW3rywYUSCreQSsgcvG+7A+ZA0oQAHFkUPSpj7Y1VlvY2q/9gf/sosa5u2W/m8vezIFHIw
cR0P/wRV95kahzy6qDWtqQ2lrFQdyDNkxhfv4nWH2gNlsYGHLhCNcoVD2EFzpQ9D1TYA3RooLc/3
+hgRA4b6w4bb//6C/+Lcq86Dn7EWniGSItN6sUNtVW6wzMABmgjBy3AlUHqlTo6//w6ss++nF2kw
+0qfml4vqLeuAs2VEFNMxOwixvrUSMbatK8ML/H1mG+DOgumTOtKqBEGP5VkkmTdzVYcKPTL2lmx
CPWr+E2t6ESTC0Cfabjf/CPzM0AAAACQQZ5CeIZ/ASnjkFJr99XbE6D6jeDxv1IggBX9SVos6aZ0
vknnQzcZP8yqvtkxw/YSlTgWxrufD+4vN9s3+osMDrkCRPKtUyMv2l5Bz3lG4x0IUxFSHiqIpB4t
ZM7JzIfR4xf8SbPrTZJYxHPdgIAbZq9At1WUseLRY0agwAB+75MO2gBDnK9Xtn8n2p/TOZvjAAAA
LAGeYXRCvwIx+6+T/8b4m100p8AYXgpcTSoEeAxsYId4jjrcu/0kBN6xuMmQAAAAXwGeY2pCvwIL
YN3FLOONan82Tsg8oMX6FnxkgJK0rvXfkPGUJtBY9ZK7oxABD4Yvw3TmFdcXc8TKRtJV6/yVwOmS
hSQHSmKZIZ4yECwOw2ACy/D/inFkGtVgABM5ttThAAAB8EGaaEmoQWiZTAh///6plgUg2RwBNdS7
TmZazA8FZe3mk1W1gmlG8K/2MyIldBlnRSdktWRgN6v+rRqIWmZSITBfmZlwUrQka+9CRv10CrLz
Uu5gETnmtdpJ1px26RPqV2hEcry0D+pP9kzqWB35V2OraqOaLFGBjcN/C0yg6gMXBvuBG/8JFd+n
WDDpGwzQaGTtqsOeyL4e/a8eFWreYT7gqrfyDPaS96CWXUh9mREZqvFdBUQmo9p9KP1OkY5G9KW/
+GEKOUobLPg6zsqUuoZxXJqnP8QP/02yeBteTeSQeihDth1umqKXxTcLxpItUWRlBToAqtuMNHYW
sB39DscPv9/2qkpBPuqFAsR1+Pb7ZSglKS07wQnrKuSWMryIzRXTNj/vxJgeFRDisRt+ECryqJQb
uKGWIDO8l7UllW0ESpBjsQPr6GKJM8CLjX4Iv1/qasbJ1hZYDY9ByCajU8Kh3Ob4Nd3iySpJngZ6
gcFugWMc44XcnHh+4cmx/w/6kWkK/bSkSwzRtLmsHFhXkPrqMQw0srywMU3ZHyZ5LB8PziQyXKXL
l8PbmymXpOux11qCqKU17+3qWn7/OL3Uo09MJGZg7c9lHw+IJsGiVKHYUYVogNWlFi6AbRoxmUdJ
FMYiuXyUBj1DRD4Fqq5BUUEAAACbQZ6GRREsM/8BXwC+jhLCQVClhMXQtbFWTWqtcil4e+oS7/Je
pcpHqL1gAHB5wtY51wBMO89HdIo9FKC6ur/RTwotpF2oNWIQ1lNOVaKaHZDSQRifIgddTCqXjlFb
XM1+s8yR3md8zJ381JctJv3t0C1yifvUJ4kxh0n9QmswYG7x64iT9j+kX8G4hga1JwC5NbD8A125
djCeZsEAAABjAZ6ldEK/AnT8uBefAvxEiLWEYL6CSwTe45IqZkCxFqVswpqGXt6wAGyMjvgxVzwA
9cLERPljYpyvv5RrnaiSkzo9gHvhavpq28apwbbalxgJG0ncCNGiaV0ELdywOsZcOr0xAAAAOgGe
p2pCvwILXuVGNQzJu7+DT5Xg37+pfr8ALHFv+hIm/RBLJ2J3JylYTISBari2ALusag69ITm8T4AA
AAGBQZqsSahBbJlMCHf//qmWAuXANm68t95ViXv7aMRCYsAETrfPmhCZfukA4GW/pfxJmGMSFp0u
kZTFabXZTxU2Ynrgd0s/RCwY6wNI7Hi1QNgMFEu8B5fEaAPOIEv7brf/6eDx2MKiw3j6cR9x8KHj
n7gnqBIp30KPTGHaGXozCjB3H6MzwTcEtPsjaJU1Fd5WvevkudbUfpcp2kRnwMfhDnRZ9CDsHEvX
Kr/D7daLTlctpwTdSpoE/lRgQOlaXUPPrWrkZ/1MwcMllw3y28RCPBoPlrVbg5rbiYdkYmVealZj
Qr/vdu+gVqz0IDxifyRTuSxdhlLUnMdkHF8sAHhykYHP2wLBt/79+GML/ZxldR2/4SYbKnfKj7Qs
GgkDhEnFI5v1JSAM74UWCwebCVBe+KYonxNGV5hFz/HGQ8/uXXB01N9W2059Dhj9q8JJPPgoEcFj
DzXX3AWoYXjm9Gskhw630xq8pk1z1+TS3JrFSFYZ6AgrOiVGBjGlUrGWsSqOgAAAAIhBnspFFSwz
/wEe+FBVkg3V6dmAB2f3c+NWDp7oh2kXKJKyijaVNiV5KuBWvu3G809U/xAw3jX9Nr/kV7kb/RGx
hy+yya/vAyDGQaVBp20AyTjUDnciupUMPacG9ti6VSogL1vMUkL5Za8KsRewSCTDUQETvsVIHy1P
Y2llLj/DEqGsQl76i7HZAAAASwGe6XRCvwIKlsI/m44YUjs3ds96OzPNMiLRck0IAJ1WhlrOV6Os
gEKoAeNDl+IAQlmEb+/lqDu264HnI4cbPjyRpN1QJyDb0jiByQAAAHoBnutqQr8B+auKWb6xUst3
aGO4eY9r3NDN93fhH9gANnve2LX9sTxTtzpaTvWTW46DRt8CWzX7vwhybLoGLY1IbcizDWTBp/6l
F0kVPSg3s2GRrbaDN4V5LvJPIfmS9sVse264SF8RD2Bw13TQV1jD2UJhPhBp3JWIcAAAAaBBmvBJ
qEFsmUwId//+qZYCY9KhGMBXE0jd6f/hBoIBqj/FO1hCs6zwqppbOv+hEShGx3/yPBThmUzAr2s4
5zCZtGVwHAHtAIcduHIWwJ2CzQ71vbW4daOkAxnY9Ir56/dy/446jgkrfQqVJ4Gi+BgEd12YDcss
VDAhAAADAOE/EQanU8+YCxElPF7dftcmS7jVTuVM+h9DVacdayHXsjbLoZUqdh4/HbbHBJYnnyzV
OdW5VnVyLnLsld1rwUYw2ikSqj2TLX2SFllE/d3dNex+y/xjEa4Q/oWCIKiiD3+PIfA4vWW4N0cx
a5xCgxvwkd1VH3/2yfWUee7BpDDsm0TRcJfELjaU8TzzYmdlDBbbBlCzOgY0wuIN3xZD0pFjB+xu
FYPJjpiUICcQCZrhcodpyTmMtp3s3BCr6wbcm1NU3CX8079MSjkCwYNekF9XC1ONzRQvl/8G7a8M
Era0KI1abDnC5sqDZyc/lgUNvkyTv3y7osq7ot3eeGEu10tlz/994qSyVB+cHw9qFaE5dg3dBvYG
l3HVSnb8eYed04o/kQAAATRBnw5FFSwz/wEVYaomu70jiogOCk6ABKAD912rLNsHuMg+I+bWMGZ/
D7lEjzgzop9UDdd5ThlL+7bRukOo0qP7E9jxuSW3mmnwy5GlniXZjWi9VIAbDncPIBakWLCIiTeB
6O53+Mf95O7rbGb2JIJGAwpLf54yS9LEBnnLcfgGlCvjy7IRkeBesmSIL5e6GLvteoTXzJM3P5bh
768Ck4+P/bjA0eSX2Y8xbsJAprtdkPnciIRLKpji8pbTlTK7dxagJY6VOapZlN3OuAnp3j4PS5Nv
w6kT6QNfQS3ylkEDQVACEEseRr/QysZC2aeN4+yygEYUrb5QzOxaCrACFJWXadZq4J5jfarNCpuD
JY5l6N7HRyyFor72wymzbmwRQwnib7rKkJ0fJXEP7FOHbnvI3teYgQAAAEQBny10Qr8B+ObIBA/Y
UZWSLsbyw9B4thAJRtxTnEunaea16+n6G93UOHVX5REFMY9k9tNls7t/9083URnNxc2/VQAIfQAA
AKgBny9qQr8B+bEXmTnmuYCWQAmmfgTbQD5K9oiOZNDiVztnl/VwgN8AdFsEh8/b4lmjfHBRI09T
5fDo4CVMJFtezkBgcn+OuN1btmc4/iw+NYkmIyO0KVe1PAmDyvvwAC+ZGPb5zy4Hb6ssNf9u1krC
x40uTsgkHte3rD9is2twOndxLhAKJcJa58uAKJkNymd5qOP/nzPwMzsE0nGPHr0XUjOR40kS4XAA
AADsQZsxSahBbJlMCH///qmWAIwfNUAUGMH+zWpUweukDWH0ujDK8ovuDEm9rKWlkrrh78imzIHl
ACZyx+9Nb3o+sSYX9CxrGBk6sE1DnYo1X05+MZ7C2lGy3PP8zZ8CZ/QblzaIiKJa8j2mbw3gz53u
07wLCyj56mYVlhpi2laB83ylIV9yxcXP9Ju5TMGkYr5eFYh9f4bU7l8HxRTlRruoLvNdcp/VYvW6
bNJYqfYUfwNm410BfxSDPs/HN+Sczdw31rWTxazAAALP6G29LCwAJ1kvZfMmp23qhajFAgkisyUw
lWQ1VKQxFi9oynsAAAHNQZtVSeEKUmUwId/+qZYACu/Ao/v89nN5RC4AdGF6ggIYcrJUi58WHpsN
DoSXX4Mq5n+8PL2eSGT5lZggZGxPGSU0qSx/behxo0au2LVQJ7CnX1IaxZLjyIGOPbCM38VnFeKM
A69tLMdAB5PzDXnun0Jjd/i2RfZu8bQH4xMcuRIdTJ9MmIeBQD/ylkB1v63T/w9LM5H6hdLFSAMa
YAyZu5tBq9J55+xARaPEa2hu17Gf8Psntd8Fk6DLcqjwKAz7BI6ZGG5IcHAnOhieZQczYPVvolhX
BoRbh6bb5dy6YoYYtF5iEBCisJYZYlvhSlahFRITHIA3Eh5Vp2NnVQ6puEEVdSp74CvGILRPq40J
QFj7lpeo45je/hfgPmXqb2Nb0+Y+hr3mkwJOFe429q5RNVsx6uBKGmONLUFa0q0WXgXiDezp5h90
F7PE283l25dsu7jt+JZCnoPqU+ZhubxIcBOaMOZzqTr3NNTe8kHUGQ0Bir+2DNmLJrAOKwb/QKs7
ukhVCn1knjp97CXCHQ2da9WfGQ2Qpc527AIGx9V9i+GYg+Oe49k1HbVLIP4U2pZWzdqFwoV6NIRY
OAIA4hs5DuKJK2sCriN/w6naJCEAAABXQZ9zRTRMM/8BFU39Cq7F1kN0hhKLL1Lp9hpdk9UQX1ez
nDwQazuyRBH1dI1EXhrlCAvwW36lgA0N3acRPgkD+XXDdMJhL/p/kmdyASK+qkh6loTdQN2AAAAA
KgGfknRCvwH46GFWSV29vq8jpVKX23kcyAOZTleFm1xBvgEJOB51XzSyEAAAAGoBn5RqQr8B+a/n
RAcDACUMLkeecwuCGzFW75VmzWQuVuezcnFnxcnXvsT+6dOCO9E27QwbED9Nsl0ZYEWmyEflkSOq
9M5THcbOR3x3mu8U4yMUbyErGcp71lzzSOqg/b6bAsWQKGK82kZlAAABhUGbmUmoQWiZTAh3//6p
lgApRkRwANFZ7nM//1+/+GdG0b/yHYHr5gHl2FXM+u9Oi1psPz2U4Zh7RdkT00hStDAArQxDqyA0
g5zHf/v06g09otcC9jQdadAotxjw6EC9YbGYIXqkz7vkpUAOi6XUs0I01Zx/CbGGCs4645wrFS++
6+j/H16n2Ag9yVe21oRCTNxCP9X//HPdheilJT572uQ96gZUEGEBZcU7q+zMxTBTENFIbedAbPmf
A0crffmHJ4Lxs1KY5SIu+oa7+T9Led4haf6hLvQBVnUalpdAZSJUTgMym7nfv9thu3TB+CiMolBr
7ijrMzqPw1BLd9sbbmvPFEnaIgmxGCj3x9Gxzjkb8p4ijaJFJ2vV8kvNBReEb97BpSannpX/tP7/
ZPaz2eNKVBwNUD3ZxGk/bULJXjPrG89kCDZ91kZIk5idgtVlpcBp0hxKAi5NYTXoVRg6z27Uj2t6
LkFimH944d+RS/XSBIp+zxFFA7WaUELVBQXvFaKf7A64AAAAr0Gft0URLDP/ARVhx/sY4+N3/B5P
SmkvzFnp2MlgA+zOFvNAxtcRVAM8WacY8HWtN6wcnaLl3RF8PZJZVfpAoASQH0vqilB71Obf72UX
x8jNqbvrCDbRvb0FdCY2we/VxvFVhn7/c7LAPnRef4b4bi/Stqaj3QI3862Q0harQOGXZNWmORqi
EQh8DQeA00P2P/EzvBuId67E72d/ByQHrJbt31XgvutYXpJgtnd25p0AAABKAZ/WdEK/AfjoX+sk
rvwl2QLPy6kabAECtmsOaa9lsIpbpZM1vN6lfVMJjMIU+VMAIM70ek1HybTcluRK+yXAUQSJ9oqD
UJYuB0UAAABHAZ/YakK/Afmv8UoPi7sPZTaSQmY8VYgpjs6Z8wEi+4tijOVkg+AhoyxAB/8y1U1Q
Ju4y9/J9hybWn78o6yVYgO2A1sGt8UwAAADnQZvaSahBbJlMCH///qmWACcLNzBe6UsBjMAJT6eE
U7GEWR9xsIkxT6qMSQ8cP04ExMfwnyf1Ur0BeS1FHX0exxvaS633TxOG0W63/7njib32h3FTo6RX
+k7dB/1WnuqlX5qZn0dfDOHaCatlphRZo086ZmFS5N+p8tqA4a2Q5YN6xSWLHgCY+lZerbLxMYa1
J7BFBJti7bM3kHO2xacD+mK5A4jyG0jkk/Myf8A+3wM4gSRSG2HeK+8BJbNAMm4FHRAgHQb0mVbw
l0HXI9mX680RX/g2b3SB64Zl68RmlWGQHPEg3o11AAABm0Gb/knhClJlMCH//qmWACl/CtrxpGWa
0J7iASvH+rkf6bqb2d+weFFwO8LnEJKVac8k+17qJaY5Sg3ucPOnHbN4d4E9cvaLgwwoO+iuCXa/
2xFOxGGJJAt4yxVZoUaiFZXwAu2DA0S8u5L67zdLnRRWHKggLCuGvfwZPuqGazkxoI+f+NBU1sdv
DPnIdGsqHmmS/2eYuHqRGuFyfAqgemBUR4ycENRyjzQ+tezoGvs8w+pYxav273OrEWs9UvGaTcBd
/tDmpxy0faj4M6Hs+zlr0WETmowWF020sEXgMY2+//8TiEEAuj2opJxaICqnQ1vT2R56dnfMCXqq
FCDyE/I3kTcz5WnwuQU32RrZSkli8sZo8vEkUDdFCX5uGwsZ6+58iAx8M21hoOqoQ8JDvGa8dihL
XttSR0VJkp+B8I4k2xhTmkBUQZGk8CSUPMVDwbRkGtWpLH4NKh3qt5n/p7SxPhiZYt96Vu0ICixg
nMKwgHeDkX5+gFjuXVNBFNtY/v9NqqA49HTIb+NEMDH2zmYGmZLujArEnIZmxAAAASNBnhxFNEwz
/wEVTf12uxah3bmAAD/oYpnbxoUNbQsrFT3rFeRBRlbyhZAFAeF+9RihqwiG0RM/2WMgfMRpdY2D
qi4M+fwwlpfsJTln5M6rWmWEbf/+ZZgt/KhYtpDo/nif4BhIJNaaMwLuYJ0r9EsISz8trMQxTyJF
EkYhM5Th6Ap69vtxLYoPs8RhVwu0qGwG5Lk71xn9ic8gNYla9a5MuzPBWM+0pkv5h9VS3CdThfyg
oVsUWSPFcsLQEiCKXtDbuLU83lxjJZqOLwop/JWTfBbAg+3oNP/Xv+83d3u8Sg5ltDsyRABskpmC
gp02P+8weD6n5hcod1/6l8VV4DYF5saYvOfmUbRacYhuj83CtTVf9wZh9bTmdGfA1z67CqjOapUA
AABqAZ47dEK/AfjoaUkoDK0X62h1uYAAH93VcQj9N/3+jpAiFoge7qSNZPwRSvNDdlCBiOmhYdHo
ohzhkUQ3jKJyrsxqYPp20TLDv0Vw8qIfDKb3/iQ1o/bLeEEARG3HIrzfaKMSJZPVdWmogQAAAHwB
nj1qQr8B+a/xAg9011NN+N7dIwMqQAASrnFiT6iFuXa/j/YJuenVnGkE1fFbB1KHmrAKUsK1+dSe
slRBrh+fX8UH3yndkVIMEcAaRk/gjfShQlUNOsFX1rCm370BzhjLOSe08wzkNiy48Jlkhyltj3oI
8ht99pEQxTBgAAABoUGaIkmoQWiZTAh///6plgAjCO3NAIO6BfHrbvM9Dj7NNPY+yUueet4FR9uW
/RJ/mw47RA3YioT7ECKxe/gyrmgOYhEPjQ97lxpCBkZmgbV4JAEEOH/aKYUwMk340jryxCctaZLj
oIGOPpJTLdzKWu70PsWlbGd0eoAXzsUgt9QkdnpYklb8d6RUfA0msCFbJjwjNMPiVkjoIUXxgqi1
fZA2BIUrIqFaKLQPuxjgFCRYs6ILGJPP2TCqr5EW0N2vvb/h9k9c3/lnRAIl9eJ0TUEVa2b+u9Es
MDpvgSF+z4ldbm+eXDy4BNwTXHa+W1plDDFv1MQgH9IN8SuGwa7A4rgubEXpVpxIcMR1APXYO21c
02bFk4JwIQMmVCOZauv9EDxUUn4E9yn3ApVmSxI2HOGoRe7/AxFn5Clt3s2nEoNqEGTgqSD5I//3
rQ8ifwg+UGDqr4Zs7IgR8oNxJeJoIn+bPhtCTlWfGJzWhWbcauO1mKo1ZwCVJ6tl1DPNRY+wiY9R
8tCI4j+SIFCvRpQswYutMMXKUA1ISStQLT5oziq3HAAAAGNBnkBFESwz/wEVYcfdm3IkKc6EdX/R
v3kzkYUIiL1vi5IzvfiIG9sLKIL/JpqR6oAgwHlcKSsAB2qWfK+m2njUAIgLa+QpXxD4J192VvM2
vBJLlgNlU7oGk3XJ84rCIQqBEVEAAABBAZ5/dEK/AfjoZ6pV3UiVxHYbFh7oyJrehQ4T4SFAWPlW
vYACC8y1U1QJu4y9/J/0VTIBN0qNpbbUBsCPlau6g1YAAAA2AZ5hakK/Afmv7AqLV2/OiaSSO707
5SrMZJgswDNzAc23/5s08DQpbrLAAg8/2eFKCqo9AYYlAAABoUGaZkmoQWyZTAh///6plgAUo0P1
AAybn+eRTw0ue4f/X/b3VlpkrRFkzdwQ4IgkkO6dzZAfpeMfu0IFBcP/d9RB/AWYb327UPit+R/P
yUmQ6fkV8Az1EvwSN5azTNZkec8H9g+jUDvpUKLNSLF41SnQzOmW0gS9v0xxmWF//w8M6WSENUck
RP5DpJXIvjr2sP6i9TQWULNWHlgGYGwnseOqL5c0y5uMTVIXmrzcQJIvawINehoyCcxXQbG+JLyl
R+Axvupmv5LKoELU19oYj2vooa9vCCERREvTYTkBsSIUjzwCLGm+FXHzF8NcqgUogS1kk2EOz0Ev
+JWa8kMaBmgzbrqPB/ldwXK5xSTpF0qnqM2U/nbatw6IWfxOtY6RcB7G6Lhk8ncnmLISzHnsJwT6
7aoJsXQN2XduinC1vJGTwhSpNHNui5f7ZB2D4UZHRb1BaSaeob5K+0AQ6sOQcnImVPXE3WszlQ+Q
mrn1USUwHvxROn18dOGmVhxP23N5Xie9f4WMBfHvc8pm9Yqv7Cammr3b5FdQB00FrevJQMMKQAAA
AJtBnoRFFSwz/wEVYceUHZhnzsKvclZfRVjxW/koABb4SLeaBjeBdoL6YRfMBVtyzanoudJRQI5z
0L13a8wlkiOi1FwHmkbBstWvGGqU7/x0rFXp1FmXP/c8coYFR+FMw3w933EHENStxEmgDF1DF0bO
2vt59wo1TjUFNbjMn85XWBGRJ+x/SL+DcQwIINcBikpy0AmvWC9cD/CtWQAAAFABnqN0Qr8B+Ohk
CJpdcYeVIoWx2X6M1qsdgnkkoI2GhUCkGLYUoYQHAOSW/Db6vYi0CNe/SAELhbwxqK3yC0GIgn28
RVk325Hl01tVwB2w6QAAAEkBnqVqQr8B+a/sCocWvzkAI4zAiul5J8OsXqeS8FD1aNv7u2CEJVTM
Z4opM/HrzCFlwABDYVRiOU1ud8i2cX/fF4CNWj5Ou6qBAAABXUGaqkmoQWyZTAh///6plgAUv4Vt
dkGZvTNAbt9U7AUt7wI//EoujPQE9h/BaimZ5eq2zVa37zQZGPZwgCO2/mcdP7sMKm4gs3rUr4H+
DSu6hoxoI+f7ZqKT9HlPWM/Kqp5687UT58HcHOpGuKA9PL2HDBU12CWFH3MrOZT/8YS/XwC6fkww
6ChzehQPquhxpS/WVJefyEpfnBnW46lPi4uqAZ4IdhJwDo+//OQs5J8U/sLOLR9cQuKHTJjbv18Z
9IMrlIvHnQSOdGpkUb5Qh9n0HZPu9g1xzzmvBA/08mPe/Mn5ZkDYRiX3Jq/InYOrrByXOxjo1gxY
X1hnfpi2g422YQMRScnzHQ/m1Xm8dzcT8tbiPCX6eYKhzrrjwPu/GDVfs2kjgqQ4FMlPyIKKKULC
jDtpfR5v1qHOYu9xVtRsvmi/qRPxSe8atdk1WXjIm95ohOry3LWMK66hzMEAAADpQZ7IRRUsM/8B
FWHHlB2KnXhI3g4IwekimRQjovG6PiNLg8ZqIzxD5R1a1R/2wcj2VKR3iq5+FTtiLVa538Q64Dfm
UzrQQ1Nt//7OJYKmODeN1ESvsX4GAuiWCA6bbJHh5AjRzC207zJbKbIdn0R/C6cCf1HjWJyyV3OB
5MWwsLdlENznXn0YVaEYWAugM4K1NOcyBz0tsh/WiSltbxTdfgdQxR2Rm+YrxtqFZiljEHe8mlYx
Mb/I5VNzb/9uPHV4RC5OjHLSIdbSRYmAMSW7o7YfmW9xA9g/DrHnM7urKDtpheohuhunx/oAAABR
AZ7ndEK/AfjoZAif08YlZkNMw0c6MIHNdNEhzpye1CmytySHsfu/bY97+jbiHES/UAG0BZG/v5ag
7tuuB1RJw/C414rfxT9EcPTGPdYxey9iAAAARgGe6WpCvwH5r+wKhchE47XIvHdOZd7LJpiRyb8Q
8HaYM2yt3XUisbuDKV1bA9smYQBXiHW1rpZzQxNm84F4MNSRAeO8R80AAAF6QZruSahBbJlMCH//
/qmWAALt020AFykqaNBRoVtHCM8bu/EPJi98D/Bq+TFXpQxFUr7QC9cH2MR8f0ChKVX7f8eHxcd4
wXzAOQ7VmrLj1MZ+tk1lXSHjAtNmOXW/YuDt5AVs/hgJkXFefTB4s6oRMURYvX8XWEDs5U6xsPFn
1Lbf1ALwMq4nD/hu8bp/CjSgHJoRbgYs1ZZ6/F1oOMkhxoLgAVnwG7+wbeT7GbWEpGM6V/lSaVBb
Ory3gwlpvFO0aWwTfJohKhbz2mm7BFXkhgxjFmU3Z3wyYfT1AKsEWV7E1rSLM8s1a8dQXPINsSgZ
iOVhIvoOSq8yjhVr2qpbbZYBCtKRiM23a+pUQGefsLYckPAMcdlHM2L9e+yrP5pERDRaKPnybY1E
ZcIyW4taYb21qkXcStNRhJ+FMQhgnEuxWp/rfXLQIkMZ2dwtIgDro2TBfZ/WXoLbmRhYVjVrKLso
Fk7gEDBJLFTWDn3bGsJGZSWBBlW/TVP6AAAAYUGfDEUVLDP/ARVhx5QdpLJCJyRIpURWnpHf4FyD
4SlZBCghlPMcScPLO3fvOuopKnixLj22gBCgIk/Y/o9Ct8w4iH1B5lTH7YIUKbRH1UTgFP4jli2t
4puvs1y6hZM8jIAAAABCAZ8rdEK/AfjoZAiZYy90eWpmCruhxwcSX9zZRABpWsxU1QJu4y9/J/3B
Tao7vLCE2t9G8PxaKGwGG2NwstTMIBlRAAAAMgGfLWpCvwH5r+wKirnpxhV5sNQn82bHeuANgzgo
SmRq0nyX3XwAgm2q2GkMNZkfFq6NAAABdkGbMkmoQWyZTAh///6plgAFcMk+gAhln3nw6ajdO8Mh
g5N/+H5KdHBl0zAtzUzGgs/58Ya6Lik8Zo0h+F/yxddx52WfTgM6w7bl7VTs9H9GylkZZ1zPD5qJ
J+FUrvJnLj1yJtHzZI2G2Ba96lmibm6xxfT0i1+eH4mqvvg9qi0b0aCB8dgO/YvnJxVTNEKFbdiI
6KYFj18oscg9xA7Qs+6QzTm/AEU4TuMShlg09bOd0yIY0u+UctVLLRGRkMDT/zgA3LRT/tK5X985
d4tgBoaI5Ig3Qvv4Fj+xx9OcDsSwudqPgpTYX4r9bMYhVlU+5oS0FMeI1JwiYFNcqjeN06ECXHe7
zFeBvtcDWkmoov4aVxQQJcD/l3WVjlwBQ/uAstmeawv1bj4ofaNSdy2+00kWjY7CDuiNPdqfBA32
J8KWSaxoz/U2KnPsrNFZkvVjBoY3ZS5SKGTaTjOmm3jBhzbNQYLa5KHezMIzpWcosr6XJ597FsKx
AAAAsUGfUEUVLDP/ARVhx5Qdpl8QrrCeezbKmgAWtp8UdhK9R1K8eFt8HB1ZloWNn2yTz358YJ5v
eh8vTVuSrecAvXbhsr+6hAG7nR5abPf7MTP2UGU4c9PY6IacBRxxFHaOewTK+Xc967w1vXa7zA4R
Yd/94WWndj3uUmoA3g//BH/o3d91AtlTZbemTbV+ZGeTTBbRops3wJRgnrv4qA+ZVZBL83kGRuF9
RA7W+Xs42xqLNgAAAEUBn290Qr8B+OhkCJnZIqsl9AouPYsWoJQvZUGdRhE3tPyh80LYifIYn1H2
HgBCdXpNR6GFQQAq0CdWmfQDtwMFhyl6fN4AAABWAZ9xakK/Afmv7AqLV2vbtUL6kTCLUdAbOjwJ
g9shlNFBmZaKz+ru8kXA2dtRiFDM+2Ez95UH4WvgAhsKoxHKa3Ok1NsyQa4wQTPOxejEf8Hj5H4P
8EEAAAEUQZt2SahBbJlMCH///qmWAArvwrjTIziNMqIBPVkABU30CmZ9n7QJGfHU14hAmvE5WLzy
sH8qD8xhZYRlrvVMYhK3h3t4fwyF5+t5DAi4L5L8eIXOWDqV0R96E9pahP0FeTF7WzET7uoUdoDU
eyimfDMrOtqcL0UuMxmOfPg7g51I1xTmp9opj3I2EGkwAb7HV8QbsBZIA1gnHdlhhF2Y7+ga5gBU
qnQb+2TCFRLe4qPctvn093ExQMwT2Rrf/8Oa7koHPm60evmXpLhGGKBBtvepI/EhX2Q40b8PIiI5
zpjhGNtmemLiU2xUo4rOlei7BWj8Nj0OGpe/KU8FS0RKc6o1n/XogA4eG4BWfWijME68gsfEAAAA
00GflEUVLDP/ARVhx5QdplsbC+Rzl37GnBrSF2WdncXUdmc2QJA6CctbM2R6F/xbAqADaj7mMxDQ
cv5YmBrH4OTZF06+ov/kl/Ox4qNStlTuRuWcIRTd5zoIwRckUSW+5Wk/SoCQxmfRFQ0NA72SPCfC
9RTBXOdqIMkgkOFHUQTNSbUi+yZ+tyGxKiRwDROoIJWf1/WSV2U/5n0mxmyIiYnyw0K6svhgVpfL
RJvA9fGvFOUTXkGaq0eHlcCqmJDP28dXZ7n4NvfMJe0ELhqpVUJJrOIAAABkAZ+zdEK/AfjoZAia
XXCpThUgScFHIvacwCS06ME0MFRIHKDU8h45IDSLQx0DVVBlBEgYKXhNuHqfywbO2JSG/v5ag7tu
uB5OJw/C414rfxTNOHFvWWY2ptMiSDOLgHQrD9VVWQAAACoBn7VqQr8B+a/sCopOigCYsTh9rju6
0CgAfubu1FaJURK5BHTrffSwLqAAAAFMQZu6SahBbJlMCHf//qmWAALtxgkAFQJWU5z8LlrW6ulU
KCij7zYKmDwOdglmPpIzYIj5t4XZyXtvQ41MoYayiLx9RqniQsUlH3ox2R/mcbjNh2AXEej4QeYk
kQPOAtZrDT1k9vPluirjTgsEW7IqO2wxwdzPbZo3t4zIJFLQ8NPF3xBQBQjnheihK2aI8Phxes2c
1PRonbEEoLpBeSqsHjbU0m3r+2R7fzUGFCCTNHVvp2TcrYCgmHxBosmqMw+NFBxebxrZwYJ2UJuw
2DG7absQc2HHJ0znM4NLKNuFSBIi40x8F87OX+RVcUE7O83C03Z53dkms2bgX7EMMNDjOs0kVyGV
Aja/RCy1EOD1T5C71Y9ZP91p04rIukQWZ41zNX18OUv+uLkCzDZ1zuLIAAAMvkMXYEAFRVRSkSX8
A+McR2nA1ilfS287zEEAAACGQZ/YRRUsM/8BFWHHlB2iYHJ+Ymfk4APvSpvyUdEbxg+fd42+kqN+
ULGzE0NdL8W3mT687lCUMQX9IOoi3Ug7w1oDmrKZOW9Pgnv9mJhKNn+iubXq6YM0DeoSr/EJiZLQ
wwrApGDn0CuQL8N4fWGOJ/MFfn9pMYxv4wYjRxdUR3z8BGMRhz0AAAA9AZ/3dEK/AfjoZAiY5AYP
gJiHIzKD5PSUqxYAjh6yJ3tXNpM3MgWXiZVc5gBD2F5Y11kz2mkxYLFyY6klsAAAAEIBn/lqQr8B
+a/sCopOljE3luqqsIJBTGTgWJZd+erfznr5V1GzwqbGGu4okzmx2HYFEvHFAT3OeyvHWv5TA93g
7kkAAACJQZv+SahBbJlMCHf//qmWAALx7y39LnQX/waHHiAINLx9XaM3LnjpkNLiAR9NbGqeSYrG
6a/GwTB/vlotE1SI8nsYdhn37oCjWDqUhlSxBZ31Yo35WxuHWC55TmrmHWRDrNWBgivW/Rt3WcV0
qDTSBwklISsHF02ckTmykwlhltm5Ea5IWhGCSZkAAADKQZ4cRRUsM/8BFWHHlB2iYHJ+YmXLeXTw
T4xNw0N4cIsEuOdUmYsHNR4sqzpXwARB68YzENBy/liYGsfg5NkXTr6i/+SX87Hio1K2VO5G5Zwh
FN3nOgjBFyRRJb7laT9KgJDGZ64FCeWce1Mcj42f7msLBkkJRN/MogYFkFae6xrhgC64kcA0To7w
V2ZfrJK7Kf8z6TYzZERMT5YaFdWCZhOUrRKl4EPYe/6un215UWqtHh5Wk4/u4DVGeXxg5JXZOqm3
XbGbdcG6pQAAAGkBnjt0Qr8B+OhkCJjkBerFozdDIjYjTXFgf/GGfX8VdxHxfApIDSK12QuqPn78
1gLPGZDXF6k3rnFiRtjJOOjywBNAIl93tlWtpTz59YNWWkMjGgXbMAh8MzjRtd8BDi/HEUBqrEZy
ubEAAAAyAZ49akK/Afmv7AqKToD4HI7vThu0/OoRrsLcRMg+JhjdYgBKhhjUd2N4bjYnqwUeDGgA
AAA+QZoiSahBbJlMCHf//qmWAABirmip94CxDYRdcjGT0YKxqAD7ogmBcj2Lh3cstbJLkvVmtuJw
AUIFFzXiv6IAAAB4QZ5ARRUsM/8BFWHHlB2iYHJ+XbpLBFKURWfnvGjbQb5y8oOu4BT00Rno4t01
7vk8AN3Ojy02e/2YmLc4S4TKJ/gh7uvke6SZG7li8TH+Sm4Mj/567PIXuOHJMk26iJS70oBD+8Ol
uUQx/rBvx1Npg+hBvNdkrtFZAAAAPwGef3RCvwH46GQImOPwF7TIbGUW1TOM5/GMec1dd1XaYJSj
dOjNC7pqPtWUAEPqX2PmcTtMFo8sCs0BAWOnZQAAADYBnmFqQr8B+a/sCopOg+A5HmhcoYDRf3n0
m2cDcBgAGaBnkgn4dmGcAENhVGI5RgGjXh4qhCsAAAAkQZpmSahBbJlMCGf//p4QAABifUVmp3fA
Dk/bjABD6wv5q/XAAAAAMEGehEUVLDP/ARVhx5QdomByfl2SQK2yNIB4MSRldYUCLhwdeLWoYah9
CFYjZuP2KQAAACEBnqN0Qr8B+OhkCJjj4K3wE1DM5v4tUOztNJiNvN+BbZEAAAAfAZ6lakK/Afmv
7AqKToD4HI7vThu0/OoRrsR8W0gfnwAAABlBmqdJqEFsmUwIV//+OEAAAMn7Q2uj97axAAAGjm1v
b3YAAABsbXZoZAAAAAAAAAAAAAAAAAAAA+gAAA4QAAEAAAEAAAAAAAAAAAAAAAABAAAAAAAAAAAA
AAAAAAAAAQAAAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAIAAAW4
dHJhawAAAFx0a2hkAAAAAwAAAAAAAAAAAAAAAQAAAAAAAA4QAAAAAAAAAAAAAAAAAAAAAAABAAAA
AAAAAAAAAAAAAAAAAQAAAAAAAAAAAAAAAAAAQAAAAAGwAAABIAAAAAAAJGVkdHMAAAAcZWxzdAAA
AAAAAAABAAAOEAAABAAAAQAAAAAFMG1kaWEAAAAgbWRoZAAAAAAAAAAAAAAAAAAAKAAAAJAAVcQA
AAAAAC1oZGxyAAAAAAAAAAB2aWRlAAAAAAAAAAAAAAAAVmlkZW9IYW5kbGVyAAAABNttaW5mAAAA
FHZtaGQAAAABAAAAAAAAAAAAAAAkZGluZgAAABxkcmVmAAAAAAAAAAEAAAAMdXJsIAAAAAEAAASb
c3RibAAAALNzdHNkAAAAAAAAAAEAAACjYXZjMQAAAAAAAAABAAAAAAAAAAAAAAAAAAAAAAGwASAA
SAAAAEgAAAAAAAAAAQAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAABj//wAAADFhdmND
AWQAFf/hABhnZAAVrNlBsJaEAAADAAQAAAMAoDxYtlgBAAZo6+PLIsAAAAAcdXVpZGtoQPJfJE/F
ujmlG88DI/MAAAAAAAAAGHN0dHMAAAAAAAAAAQAAAEgAAAIAAAAAFHN0c3MAAAAAAAAAAQAAAAEA
AAJQY3R0cwAAAAAAAABIAAAAAQAABAAAAAABAAAKAAAAAAEAAAQAAAAAAQAAAAAAAAABAAACAAAA
AAEAAAoAAAAAAQAABAAAAAABAAAAAAAAAAEAAAIAAAAAAQAACgAAAAABAAAEAAAAAAEAAAAAAAAA
AQAAAgAAAAABAAAKAAAAAAEAAAQAAAAAAQAAAAAAAAABAAACAAAAAAEAAAQAAAAAAQAACgAAAAAB
AAAEAAAAAAEAAAAAAAAAAQAAAgAAAAABAAAKAAAAAAEAAAQAAAAAAQAAAAAAAAABAAACAAAAAAEA
AAQAAAAAAQAACgAAAAABAAAEAAAAAAEAAAAAAAAAAQAAAgAAAAABAAAKAAAAAAEAAAQAAAAAAQAA
AAAAAAABAAACAAAAAAEAAAoAAAAAAQAABAAAAAABAAAAAAAAAAEAAAIAAAAAAQAACgAAAAABAAAE
AAAAAAEAAAAAAAAAAQAAAgAAAAABAAAKAAAAAAEAAAQAAAAAAQAAAAAAAAABAAACAAAAAAEAAAoA
AAAAAQAABAAAAAABAAAAAAAAAAEAAAIAAAAAAQAACgAAAAABAAAEAAAAAAEAAAAAAAAAAQAAAgAA
AAABAAAKAAAAAAEAAAQAAAAAAQAAAAAAAAABAAACAAAAAAEAAAoAAAAAAQAABAAAAAABAAAAAAAA
AAEAAAIAAAAAAQAACgAAAAABAAAEAAAAAAEAAAAAAAAAAQAAAgAAAAABAAAKAAAAAAEAAAQAAAAA
AQAAAAAAAAABAAACAAAAAAEAAAQAAAAAHHN0c2MAAAAAAAAAAQAAAAEAAABIAAAAAQAAATRzdHN6
AAAAAAAAAAAAAABIAAAHTwAAAmUAAACUAAAAMAAAAGMAAAH0AAAAnwAAAGcAAAA+AAABhQAAAIwA
AABPAAAAfgAAAaQAAAE4AAAASAAAAKwAAADwAAAB0QAAAFsAAAAuAAAAbgAAAYkAAACzAAAATgAA
AEsAAADrAAABnwAAAScAAABuAAAAgAAAAaUAAABnAAAARQAAADoAAAGlAAAAnwAAAFQAAABNAAAB
YQAAAO0AAABVAAAASgAAAX4AAABlAAAARgAAADYAAAF6AAAAtQAAAEkAAABaAAABGAAAANcAAABo
AAAALgAAAVAAAACKAAAAQQAAAEYAAACNAAAAzgAAAG0AAAA2AAAAQgAAAHwAAABDAAAAOgAAACgA
AAA0AAAAJQAAACMAAAAdAAAAFHN0Y28AAAAAAAAAAQAAACwAAABidWR0YQAAAFptZXRhAAAAAAAA
ACFoZGxyAAAAAAAAAABtZGlyYXBwbAAAAAAAAAAAAAAAAC1pbHN0AAAAJal0b28AAAAdZGF0YQAA
AAEAAAAATGF2ZjU2LjQwLjEwMQ==
">
  Your browser does not support the video tag.
</video>



## 5.7 选择排序 The Selection Sort  
选择排序在冒泡排序的基础上改进，其一次遍历只做一次交换。在一次遍历中，冒泡排序寻找最大的项，完成遍历后，将其放到合适的位置，接下来是遍历n-1项，将最大的项放到合适的位置，下面图显示了选择排序的过程，  
![selectionsortnew.png](http://interactivepython.org/courselib/static/pythonds/_images/selectionsortnew.png)  


```python
def selectionSort(alist):
    for fillSlot in range(len(alist)-1, 0, -1):
        positionOfMax = 0
        for location in range(1, fillSlot+1):
            if alist[location] > alist[positionOfMax]:
                positionOfMax = location
        
        temp = alist[fillSlot]
        alist[fillSlot] = alist[positionOfMax]
        alist[positionOfMax] = temp
```


```python
alist = [2, 5, 1, 3, 6, 9, 8, 7, 0, 4]
```


```python
selectionSort(alist)
```


```python
alist
```




    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]



和冒泡排序一样，选择排序的比较次数也为$\mathcal{O}(n^2)$，但是因为交换次数较少了，选择排序通常执行地更快。


```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation
from matplotlib import rc

# equivalent to rcParams['animation.html'] = 'html5'
rc('animation', html='html5')

fig = plt.figure()
plt.title('Selection Sort')
plt.xticks([])
plt.yticks([])

alist = [2, 5, 1, 3, 6, 9, 8, 7, 4]

color = ['gray']*len(alist)
ims = []

for fillslot in range(len(alist)-1,0,-1):
    color[fillslot] = 'blue'
    positionOfMax = 0
    color[positionOfMax] = 'yellow'
    im1 = plt.bar(np.arange(len(alist)), alist, color=color, animated=True, visible=True)
    ims.append(im1)
    for location in range(1, fillslot+1):
        color[location] = 'red'
        im2 = plt.bar(np.arange(len(alist)), alist, color=color, animated=True, visible=True)
        ims.append(im2)
        if alist[location] > alist[positionOfMax]:
            color[positionOfMax] = 'gray'
            positionOfMax = location
            color[positionOfMax] = 'yellow'
            im3 = plt.bar(np.arange(len(alist)), alist, color=color, animated=True, visible=True)
            ims.append(im3)
        else:
            color[location] = 'gray'
            im4 = plt.bar(np.arange(len(alist)), alist, color=color, animated=True, visible=True)
            ims.append(im4)
       
    temp = alist[fillslot]
    alist[fillslot] = alist[positionOfMax]
    alist[positionOfMax] = temp
    color[fillslot] = 'yellow'
    color[positionOfMax] = 'gray'
    im5 = plt.bar(np.arange(len(alist)), alist, color=color, animated=True, visible=True)
    ims.append(im5)
    color[fillslot] = 'gray'
    im6 = plt.bar(np.arange(len(alist)), alist, color=color, animated=True, visible=True)
    ims.append(im6)
    
ani = animation.ArtistAnimation(fig, ims, interval=50, blit=True, repeat_delay=1000)
ani
```




<video width="432" height="288" controls autoplay loop>
  <source type="video/mp4" src="data:video/mp4;base64,AAAAHGZ0eXBNNFYgAAACAGlzb21pc28yYXZjMQAAAAhmcmVlAABOhm1kYXQAAAKuBgX//6rcRem9
5tlIt5Ys2CDZI+7veDI2NCAtIGNvcmUgMTQ4IHIyNjQzIDVjNjU3MDQgLSBILjI2NC9NUEVHLTQg
QVZDIGNvZGVjIC0gQ29weWxlZnQgMjAwMy0yMDE1IC0gaHR0cDovL3d3dy52aWRlb2xhbi5vcmcv
eDI2NC5odG1sIC0gb3B0aW9uczogY2FiYWM9MSByZWY9MyBkZWJsb2NrPTE6MDowIGFuYWx5c2U9
MHgzOjB4MTEzIG1lPWhleCBzdWJtZT03IHBzeT0xIHBzeV9yZD0xLjAwOjAuMDAgbWl4ZWRfcmVm
PTEgbWVfcmFuZ2U9MTYgY2hyb21hX21lPTEgdHJlbGxpcz0xIDh4OGRjdD0xIGNxbT0wIGRlYWR6
b25lPTIxLDExIGZhc3RfcHNraXA9MSBjaHJvbWFfcXBfb2Zmc2V0PS0yIHRocmVhZHM9MSBsb29r
YWhlYWRfdGhyZWFkcz0xIHNsaWNlZF90aHJlYWRzPTAgbnI9MCBkZWNpbWF0ZT0xIGludGVybGFj
ZWQ9MCBibHVyYXlfY29tcGF0PTAgY29uc3RyYWluZWRfaW50cmE9MCBiZnJhbWVzPTMgYl9weXJh
bWlkPTIgYl9hZGFwdD0xIGJfYmlhcz0wIGRpcmVjdD0xIHdlaWdodGI9MSBvcGVuX2dvcD0wIHdl
aWdodHA9MiBrZXlpbnQ9MjUwIGtleWludF9taW49MjAgc2NlbmVjdXQ9NDAgaW50cmFfcmVmcmVz
aD0wIHJjX2xvb2thaGVhZD00MCByYz1jcmYgbWJ0cmVlPTEgY3JmPTIzLjAgcWNvbXA9MC42MCBx
cG1pbj0wIHFwbWF4PTY5IHFwc3RlcD00IGlwX3JhdGlvPTEuNDAgYXE9MToxLjAwAIAAAAUNZYiE
ADv//vdOvwKbRZdqA5JXCvbKpCZZuVJrAfKmAAADAAARsG58lw15rrP82sMu4wAJ+iexDYGXOIni
EaqeV0oJ+IwTjnaLhsmsRuR0CYshkAVHJ4Trn8ep7ESEqk2TcsxS1fNIsF2UC6hv4/tTfP3nRslO
SqOoxxeCtjEXxTryGq+VG8prDbUfazQIIrA8bg0bLXNG0IFwCWEhxIirHZBCInQmAjbdJw28GucI
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
LjQwLjEwMQ==
">
  Your browser does not support the video tag.
</video>



## 5.8 插入排序 The Insertion Sort  
  插入排序通过将每一个新的比较项插入到之前已经比较并排序过的项列表中合适位置，其复杂度仍然为$\mathcal{O}(n^2)$，下图为插入排序的操作流程，阴影部分表示每次遍历已经比较并排序过的子列表。  
![insertionsort.png](http://interactivepython.org/courselib/static/pythonds/_images/insertionsort.png)  
  开始时，假设0位置第一项为有序子列表，每一次遍历，将当前项与有序子列表中的元素做比较，将比它大的项移到右面，直到遇到较小的项或者子列表的一端，将当前项插入。  
![insertionpass.png](http://interactivepython.org/courselib/static/pythonds/_images/insertionpass.png)  
  比如上图所示，拥有5项的有序子列表内元素为17，26，54，77和93，当前项为31，首先与93比较，93比31大，向右移动，然后是77，54，当遇到26时，其比26大，停止比较并将31插入到当前位置，得到了有6个项的有序子列表。  
  
  插入排序仍然需要n-1次遍历来排序n个项，循环从位置1开始，到位置n-1，同时需要移动操作将项向后移动一个位置，为插入项留下空间，其与之前的交换操作有所不同，由于只有一次赋值，因此移动操作仅需交换操作近乎1/3操作。  
  
  插入排序所需最大比较次数为前n-1个整数的和，是$\mathcal{O}(n^2)$，最理想的情况为一次比较，即列表已经是有序的。


```python
def insertionSort(alist):
    for index in range(1, len(alist)):
        currentValue = alist[index]
        position = index
        
        while position > 0 and alist[position-1] > currentValue:
            alist[position] = alist[position-1]
            position = position -1 
            
        alist[position] = currentValue
```


```python
alist = [2, 5, 1, 3, 6, 9, 8, 7, 0, 4]
```


```python
insertionSort(alist)
```


```python
alist
```




    [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]




```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation
from matplotlib import rc

# equivalent to rcParams['animation.html'] = 'html5'
rc('animation', html='html5')

fig = plt.figure()
plt.title('Insertion Sort')
plt.xticks([])
plt.yticks([])

alist = [2, 5, 1, 3, 6, 9, 8, 7, 4]

color = ['gray']*len(alist)
ims = []

for index in range(1, len(alist)):
    for i in range(index):
        color[i] = 'black'
    currentValue = alist[index]
    position = index
    color[position] = 'red'    
    im1 = plt.bar(np.arange(len(alist)), alist, color=color, animated=True, visible=True)
    #plt.show()
    ims.append(im1)

    
    while position > 0 and alist[position-1] > currentValue:
        color[position] = 'red'
        color[position-1] = 'blue'
        im2 = plt.bar(np.arange(len(alist)), alist, color=color, animated=True, visible=True)
        #plt.show()
        ims.append(im2)
        alist[position] = alist[position-1]
        alist[position-1] = 0
        color[position] = 'black'
        position = position - 1
        color[position] = 'red'

        
    if position > 0:
        color[position-1] = 'blue'               
        im3 = plt.bar(np.arange(len(alist)), alist, color=color, animated=True, visible=True)
        #plt.show()
        ims.append(im3)
        color[position-1] = 'black'  
    
    alist[position] = currentValue
    color[position] = 'red'
    im4 = plt.bar(np.arange(len(alist)), alist, color=color, animated=True, visible=True)
    #plt.show()
    ims.append(im4)
    for i in range(index+1):
        color[i] = 'black'
    im5 = plt.bar(np.arange(len(alist)), alist, color=color, animated=True, visible=True)
    #plt.show()
    ims.append(im5)
    
ani = animation.ArtistAnimation(fig, ims, interval=50, blit=True, repeat_delay=1000)
ani
```




<video width="432" height="288" controls autoplay loop>
  <source type="video/mp4" src="data:video/mp4;base64,AAAAHGZ0eXBNNFYgAAACAGlzb21pc28yYXZjMQAAAAhmcmVlAAAnV21kYXQAAAKuBgX//6rcRem9
5tlIt5Ys2CDZI+7veDI2NCAtIGNvcmUgMTQ4IHIyNjQzIDVjNjU3MDQgLSBILjI2NC9NUEVHLTQg
QVZDIGNvZGVjIC0gQ29weWxlZnQgMjAwMy0yMDE1IC0gaHR0cDovL3d3dy52aWRlb2xhbi5vcmcv
eDI2NC5odG1sIC0gb3B0aW9uczogY2FiYWM9MSByZWY9MyBkZWJsb2NrPTE6MDowIGFuYWx5c2U9
MHgzOjB4MTEzIG1lPWhleCBzdWJtZT03IHBzeT0xIHBzeV9yZD0xLjAwOjAuMDAgbWl4ZWRfcmVm
PTEgbWVfcmFuZ2U9MTYgY2hyb21hX21lPTEgdHJlbGxpcz0xIDh4OGRjdD0xIGNxbT0wIGRlYWR6
b25lPTIxLDExIGZhc3RfcHNraXA9MSBjaHJvbWFfcXBfb2Zmc2V0PS0yIHRocmVhZHM9MSBsb29r
YWhlYWRfdGhyZWFkcz0xIHNsaWNlZF90aHJlYWRzPTAgbnI9MCBkZWNpbWF0ZT0xIGludGVybGFj
ZWQ9MCBibHVyYXlfY29tcGF0PTAgY29uc3RyYWluZWRfaW50cmE9MCBiZnJhbWVzPTMgYl9weXJh
bWlkPTIgYl9hZGFwdD0xIGJfYmlhcz0wIGRpcmVjdD0xIHdlaWdodGI9MSBvcGVuX2dvcD0wIHdl
aWdodHA9MiBrZXlpbnQ9MjUwIGtleWludF9taW49MjAgc2NlbmVjdXQ9NDAgaW50cmFfcmVmcmVz
aD0wIHJjX2xvb2thaGVhZD00MCByYz1jcmYgbWJ0cmVlPTEgY3JmPTIzLjAgcWNvbXA9MC42MCBx
cG1pbj0wIHFwbWF4PTY5IHFwc3RlcD00IGlwX3JhdGlvPTEuNDAgYXE9MToxLjAwAIAAAARfZYiE
ADf//vbw/gU2O5jQlxHN6J0zH78VuLo0N73OAAADAAA33OZE/sqTEmXaIVwr3ABQvxjQ92dIVQmF
5DPrTVSuvnn1IwxDaSGaOoDRAKV82AiiimBMz2B0OmV22dsmvojjyH5pYZ7ZfPtZhufAjuSzsI8e
+9s5XO0tROgfRoRToydCOEEyOUy67cGItG9/vBvZIwS0rnK1LP1SZ53dgAOBUunkiaRAtIJgU/Fe
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
AQAAAABMYXZmNTYuNDAuMTAx
">
  Your browser does not support the video tag.
</video>



## 5.9 希尔排序 The Shell Sort  
希尔排序也称递减增量排序算法，是插入排序的一种更高效的改进版本，将原来的列表拆成几个小的列表，每一个子列表分别用插入排序排序，希尔排序的关键是子列表的选择，相比将列表按相邻的项拆分，希尔排序利用步长（间隔）i，来选取元素构建子列表。  
![shellsortA.png](http://interactivepython.org/courselib/static/pythonds/_images/shellsortA.png)  
如上图所示，列表含有九个元素，我们用步长3将其分为3个子列表，每一个子列表用插入法排序，当排序完成后，得到的列表如下图所示，尽管列表并不是完全有序排列的，但是我们可以发现，它们离其本应该在的位置更近了。  
![shellsortB.png](http://interactivepython.org/courselib/static/pythonds/_images/shellsortB.png)  
接下来的一张图显示了最终利用步长为1的插入法（即标准插入排序）将列表排序，在上述操作的基础上，只需要4次移动操作。  
![shellsortC.png](http://interactivepython.org/courselib/static/pythonds/_images/shellsortC.png)  
希尔排序最主要的特性是其步长的选择，我们可以利用代码来比较选取不同的步长性能，首先，选择$\frac{n}{2}$为步长拆分列表，下一次遍历选择$\frac{n}{4}$为步长拆分列表，直到最终以1为步长的基本插入排序。下图显示了第一次遍历的以$\frac{n}{2}$为步长拆分的子列表。  
![shellsortD.png](http://interactivepython.org/courselib/static/pythonds/_images/shellsortD.png)  
下面的 `shellSort` 函数显示了每一个步长拆分下子列表的排序，最后一次排序的步长值为1。


```python
def shellSort(alist):
    sublistCount = len(alist) // 2
    while sublistCount > 0:
        for startPosition in range(sublistCount):
            gapInsertionSort(alist, startPosition, sublistCount)
            
        print('After increment of size', sublistCount, 'The list is', alist)
        
        sublistCount = sublistCount // 2
        
def gapInsertionSort(alist, start, gap):
    for i in range(start+gap, len(alist), gap):
        currentValue = alist[i]
        position = i
        
        while position >= gap and alist[position-gap] > currentValue:
            alist[position] = alist[position-gap]
            position = position - gap
            
        alist[position] = currentValue
```


```python
alist = [54, 26, 93, 17, 77, 31, 44, 55, 20]
```


```python
shellSort(alist)
```

    After increment of size 4 The list is [20, 26, 44, 17, 54, 31, 93, 55, 77]
    After increment of size 2 The list is [20, 17, 44, 26, 54, 31, 77, 55, 93]
    After increment of size 1 The list is [17, 20, 26, 31, 44, 54, 55, 77, 93]



```python
import numpy as np
import matplotlib.pyplot as plt
import matplotlib.animation as animation
from matplotlib import rc

# equivalent to rcParams['animation.html'] = 'html5'
rc('animation', html='html5')

fig = plt.figure()
plt.title('Shell Sort')
plt.xticks([])
plt.yticks([])

alist = [2, 5, 1, 3, 6, 9, 8, 7, 4]
    
color = ['gray']*len(alist)
ims = []
im1 = plt.bar(np.arange(len(alist)), alist, color=color)
#plt.show()
ims.append(im1)

def gapInsertionSort(alist, start, gap):
    for index in range(start+gap, len(alist), gap):
        color[start] = 'red'
        im2 = plt.bar(np.arange(len(alist)), alist, color=color)
        #plt.show()
        ims.append(im2)
        color[index] = 'red'
        im3 = plt.bar(np.arange(len(alist)), alist, color=color)
        #plt.show()
        ims.append(im3)
        currentValue = alist[index]
        position = index


        while position >= gap and alist[position-gap] > currentValue:
            alist[position] = alist[position-gap]
            alist[position-gap] = 0
            position = position - gap
            im4 = plt.bar(np.arange(len(alist)), alist, color=color)
            #plt.show()
            ims.append(im4)

        alist[position] = currentValue
        im5 = plt.bar(np.arange(len(alist)), alist, color=color)
        #plt.show()
        ims.append(im5)
        
    for index in range(start, len(alist), gap):
        color[index] = 'gray'
    im6 = plt.bar(np.arange(len(alist)), alist, color=color)
    #plt.show()
    ims.append(im6)

sublistCount = len(alist) // 2
while sublistCount > 0:
    for startPosition in range(sublistCount):
        gapInsertionSort(alist, startPosition, sublistCount)
        
    sublistCount = sublistCount // 2

ani = animation.ArtistAnimation(fig, ims, interval=50, blit=True, repeat_delay=1000)
ani
```




<video width="432" height="288" controls autoplay loop>
  <source type="video/mp4" src="data:video/mp4;base64,AAAAHGZ0eXBNNFYgAAACAGlzb21pc28yYXZjMQAAAAhmcmVlAAA2A21kYXQAAAKuBgX//6rcRem9
5tlIt5Ys2CDZI+7veDI2NCAtIGNvcmUgMTQ4IHIyNjQzIDVjNjU3MDQgLSBILjI2NC9NUEVHLTQg
QVZDIGNvZGVjIC0gQ29weWxlZnQgMjAwMy0yMDE1IC0gaHR0cDovL3d3dy52aWRlb2xhbi5vcmcv
eDI2NC5odG1sIC0gb3B0aW9uczogY2FiYWM9MSByZWY9MyBkZWJsb2NrPTE6MDowIGFuYWx5c2U9
MHgzOjB4MTEzIG1lPWhleCBzdWJtZT03IHBzeT0xIHBzeV9yZD0xLjAwOjAuMDAgbWl4ZWRfcmVm
PTEgbWVfcmFuZ2U9MTYgY2hyb21hX21lPTEgdHJlbGxpcz0xIDh4OGRjdD0xIGNxbT0wIGRlYWR6
b25lPTIxLDExIGZhc3RfcHNraXA9MSBjaHJvbWFfcXBfb2Zmc2V0PS0yIHRocmVhZHM9MSBsb29r
YWhlYWRfdGhyZWFkcz0xIHNsaWNlZF90aHJlYWRzPTAgbnI9MCBkZWNpbWF0ZT0xIGludGVybGFj
ZWQ9MCBibHVyYXlfY29tcGF0PTAgY29uc3RyYWluZWRfaW50cmE9MCBiZnJhbWVzPTMgYl9weXJh
bWlkPTIgYl9hZGFwdD0xIGJfYmlhcz0wIGRpcmVjdD0xIHdlaWdodGI9MSBvcGVuX2dvcD0wIHdl
aWdodHA9MiBrZXlpbnQ9MjUwIGtleWludF9taW49MjAgc2NlbmVjdXQ9NDAgaW50cmFfcmVmcmVz
aD0wIHJjX2xvb2thaGVhZD00MCByYz1jcmYgbWJ0cmVlPTEgY3JmPTIzLjAgcWNvbXA9MC42MCBx
cG1pbj0wIHFwbWF4PTY5IHFwc3RlcD00IGlwX3JhdGlvPTEuNDAgYXE9MToxLjAwAIAAAAOOZYiE
AD///vdonwKbWkN6gOSVxSXbT4H/q2dwfI/pAwAAAwAArqxz6KZIGF9dIa9GEHLOAArcx8tWWm6/
rRmf8a25RGAHGeoRrsaBlTvBJ65pknBiTtCfY2VOIBcT35rQ7WlTGFgLCXtTbi/wLizmF9ivkvIY
jSALQx9i0Lo+JR8jEx2spzGXkjXK3ZDp7CwZsjd3Eqt8UyqrV68y+Y2tT1M9oEwFrppVrtWgd02N
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
AAABAAAEAAAAAAEAAAAAAAAAAQAAAgAAAAABAAAKAAAAAAEAAAQAAAAAAQAAAAAAAAABAAACAAAA
AAEAAAoAAAAAAQAABAAAAAABAAAAAAAAAAEAAAIAAAAAAQAACgAAAAABAAAEAAAAAAEAAAAAAAAA
AQAAAgAAAAABAAAKAAAAAAEAAAQAAAAAAQAAAAAAAAABAAACAAAAAAEAAAoAAAAAAQAABAAAAAAB
AAAAAAAAAAEAAAIAAAAAAwAABAAAAAABAAAKAAAAAAEAAAQAAAAAAQAAAAAAAAABAAACAAAAAAEA
AAoAAAAAAQAABAAAAAABAAAAAAAAAAEAAAIAAAAABQAABAAAAAABAAAKAAAAAAEAAAQAAAAAAQAA
AAAAAAABAAACAAAAAAEAAAoAAAAAAQAABAAAAAABAAAAAAAAAAEAAAIAAAAAAQAACgAAAAABAAAE
AAAAAAEAAAAAAAAAAQAAAgAAAAABAAAKAAAAAAEAAAQAAAAAAQAAAAAAAAABAAACAAAAAAEAAAoA
AAAAAQAABAAAAAABAAAAAAAAAAEAAAIAAAAAAQAACgAAAAABAAAEAAAAAAEAAAAAAAAAAQAAAgAA
AAAEAAAEAAAAABxzdHNjAAAAAAAAAAEAAAABAAAATQAAAAEAAAFIc3RzegAAAAAAAAAAAAAATQAA
BkQAAAH6AAAAaAAAADcAAAAoAAAAmwAAATwAAABkAAAAagAAACAAAAF+AAAAVwAAAHIAAAAZAAAB
OQAAACoAAAAsAAAAIQAAAZIAAABLAAAAWQAAAZkAAABcAAAAIwAAAEcAAADCAAAARwAAAC4AAAAi
AAABXQAAAFUAAAAzAAAANAAAAHIAAAB9AAABIgAAAf8AAACzAAAAbAAAAJUAAAEjAAAAiAAAAFQA
AABLAAABCwAAAQkAAADhAAABnQAAAZQAAAFjAAAASgAAADQAAAAqAAABTgAAAEAAAABpAAAALwAA
AQUAAABzAAAAPAAAAGcAAAFYAAAATQAAAD4AAABTAAABOgAAAHcAAABCAAAAVAAAANQAAABcAAAA
SQAAADsAAAEBAAAAvgAAAJIAAAEYAAAAFHN0Y28AAAAAAAAAAQAAACwAAABidWR0YQAAAFptZXRh
AAAAAAAAACFoZGxyAAAAAAAAAABtZGlyYXBwbAAAAAAAAAAAAAAAAC1pbHN0AAAAJal0b28AAAAd
ZGF0YQAAAAEAAAAATGF2ZjU2LjQwLjEwMQ==
">
  Your browser does not support the video tag.
</video>



乍看之下，希尔排序在最后一步做了一次完全插入排序，可能其并不比插入操作表现更好，但是，由于之前的步进插入排序操作将列表初步排序，即该列表相比之下更有序（有点类似熵的概念，熵比较大），因此最后的插入排序不需要过多的比较和移动，操作起来更快。由于步长的选择，希尔排序的复杂度在 $\mathcal{O}(n^2)$ 和 $\mathcal{O}(n)$ 之间，比如步长为1的话，复杂度为 $\mathcal{O}(n^2)$ ，步长使用 $2^k-1(1, 3, 5, 7, ...)$的话，为 $\mathcal{O}(n^{\frac{3}{2}})$ 。  
## 5.10 归并排序 The Merge Sort  
归并排序（英语：Merge sort，或mergesort），是建立在归并操作上的一种有效的排序算法，效率为$\mathcal{O}(n\log n)$。该算法是采用分治法（Divide and Conquer）的一个非常典型的应用，递归地将列表分为两部分，直到子列表为空，才开始排序，当两个子列表排序完成后，开始归并操作——即将两个小的有序列表结合成一个新的有序列表，下面两张图分别显示了归并排序 `mergeSort` 的拆分和归并操作。  
![mergesortA.png](http://interactivepython.org/courselib/static/pythonds/_images/mergesortA.png)  
![mergesortB.png](http://interactivepython.org/courselib/static/pythonds/_images/mergesortB.png)  
函数 `mergeSort` 如下所示，终止条件是子列表的长度小于或等于1，利用Python中的 `slice` 操作将列表分为左右两部分。  


```python
def mergeSort(alist):
    # show the contents of the list being sorted at the start of each invocation
    print("Splitting", alist)
    if len(alist) > 1:
        mid = len(alist) // 2
        leftHalf = alist[:mid]
        rightHalf = alist[mid:]
        
        mergeSort(leftHalf)
        mergeSort(rightHalf)
    
        # merging the two smaller sorted lists into a larger sorted list
        i, j, k = [0, 0, 0]

        while i < len(leftHalf) and j < len(rightHalf):
            if leftHalf[i] < rightHalf[j]:
                alist[k] = leftHalf[i]
                i = i+1
            else:
                alist[k] = rightHalf[j]
                j = j+1
            k = k+1
            
        while i < len(leftHalf):
            alist[k] = leftHalf[i]
            i = i+1
            k = k+1
            
        while j < len(rightHalf):
            alist[k] = rightHalf[j]
            j = j+1
            k = k+1        
    
    # show the merging process
    print('Merging', alist)
```


```python
alist = [54,26,93,17,77,31,44,55,20]
```


```python
mergeSort(alist)
```

    Splitting [54, 26, 93, 17, 77, 31, 44, 55, 20]
    Splitting [54, 26, 93, 17]
    Splitting [54, 26]
    Splitting [54]
    Merging [54]
    Splitting [26]
    Merging [26]
    Merging [26, 54]
    Splitting [93, 17]
    Splitting [93]
    Merging [93]
    Splitting [17]
    Merging [17]
    Merging [17, 93]
    Merging [17, 26, 54, 93]
    Splitting [77, 31, 44, 55, 20]
    Splitting [77, 31]
    Splitting [77]
    Merging [77]
    Splitting [31]
    Merging [31]
    Merging [31, 77]
    Splitting [44, 55, 20]
    Splitting [44]
    Merging [44]
    Splitting [55, 20]
    Splitting [55]
    Merging [55]
    Splitting [20]
    Merging [20]
    Merging [20, 55]
    Merging [20, 44, 55]
    Merging [20, 31, 44, 55, 77]
    Merging [17, 20, 26, 31, 44, 54, 55, 77, 93]


分别考虑归并排序的拆分和归并操作，对半拆分长度为n的列表需要操作$\log n$次，归并长度为n的列表需要操作n次，总的操作次数为 $n \log n$，所以归并排序的复杂度为 $\mathcal{O}(n \log n)$。  
另外切记，切片长度为k的列表复杂度为 $\mathcal{O}(k)$，并且，函数 `mergeSort` 需要额外的空间存储列表的两半部分，当数据量大的时候，会导致一些问题。  

## 5.11 快速排序 The Quick Sort  
快速排序同样利用分治（divide and conquer）法获取更高的效率，但其无需额外的存储空间，然而代价是列表可能不会对半分拆，这回影响其效率。  
快速排序开始先选中一个值，称为关键值，选取关键值有很多方式，我们先以选取第一项为例。关键值的作用是协助分拆列表，其在最终排序好的列表中的位置为拆分点，快速排序调用该点拆分列表。  
下面图示的例子中，54作为关键值，其最终的位置在当前31所在位置，然后开始拆分操作，然后将比它小和大的值分别放到其两边。  
![firstsplit.png](http://interactivepython.org/courselib/static/pythonds/_images/firstsplit.png)  
拆分操作开始先定位两个位置标志， `leftmark` 和 `rightmark` ，位于剩下列表的开始和结束位置（图中位置1和8），其目的是将相对于关键值错序的项移动到正确位置（比关键值大或小的位置），同时关键中也趋近于拆分点，如下图所示  
![partitionA.png](http://interactivepython.org/courselib/static/pythonds/_images/partitionA.png)  
递增 `leftmark` 直到遇到比关键值大的值，然后递增 `rightmark` 直到遇到比关键值小的值，这两个值相较于拆分点错位，图中的93和20，然后交换它们的位置并继续重复以上操作。  
当 `rightmake` 小于 `leftmark` 时，终止操作， 当前`rightmark` 所处的位置即为拆分点，然后与关键值交换位置，现在拆分点左边的项都比关键值小，右边的值都比关键值大，然后，将列表拆分两半，分别递归调用快速排序。
![](http://interactivepython.org/courselib/static/pythonds/_images/partitionA.png)  
`quickSort` 函数如下所示，`quickSortHelper` 为递归函数，与归并排序的终止条件相同，即如果列表的长度小于或等于1，列表为有序的，大于1继续拆分递归排序。`patition` 函数上述操作的表示。  


```python
def quickSort(alist):
    quickSortHelper(alist, 0, len(alist)-1)
    
def quickSortHelper(alist, first, last):
    if first < last:
        splitPoint = partition(alist, first, last)
        
        quickSortHelper(alist, first, splitPoint-1)
        quickSortHelper(alist, splitPoint+1, last)
        
def partition(alist, first, last):
    pivotValue = alist[first]
    leftmark = first + 1
    rightmark = last
    
    done = False
    while not done:
        while leftmark <= rightmark and alist[leftmark] <= pivotValue:
            leftmark = leftmark + 1
        while alist[rightmark] >= pivotValue and rightmark >= leftmark:
            rightmark = rightmark - 1
            
        if rightmark < leftmark:
            done = True
        else:
            temp = alist[leftmark]
            alist[leftmark] = alist[rightmark]
            alist[rightmark] = temp
            
    temp = alist[first]
    alist[first] = alist[rightmark]
    alist[rightmark] = temp
    
    return rightmark
```


```python
alist = [54,26,93,17,77,31,44,55,20]
```


```python
quickSort(alist)
```


```python
alist
```




    [17, 20, 26, 31, 44, 54, 55, 77, 93]



分析 `quickSort` 的效率，对半拆分一个长度为n的列表需要 $\log n$ 次拆分，寻找拆分点，n个项中每一个项都需要与关键点对比，因此总的复杂度为 $n\log n$ ，并且，其不不像归并排序需要额外的空间。  
但在非理想情况下，拆分点并不总是在列表正中间，或靠右，或靠左，会将n个元素的列表分为0项和n-1项，然后将n-1项分为0项和n-2项，如此往复，这些递归总的复杂度为 $\mathcal{O}(n^2)$ 。  
之前有表，关键值的选取有不同的方法，有一种称为三数取中法（median of three），考虑列表的首尾和中间三项，例如上面列表的54，77和20。取三个数的中位数54作为关键值，该方法对于排序一些“熵”比较大的列表非常有用。

## 5.12 总结  
* 对于有序和无序列表，顺序搜索的效率皆为 $\mathcal{O}(n)$。  
* 二分查找在搜索有序列表时，表现最差，效率为$\mathcal{O}(\log n)$。  
* 散列（哈希）表为常数级搜索。  
* 冒泡排序、选择排序和插入排序的效率皆为 $\mathcal{O}(n^2)$。  
* 希尔排序在插入排序的基础上，利用步进子列表改进性能，效率为 $\mathcal{O}(n)$与 $\mathcal{O}(n^2)$之间。  
* 归并排序的效率为 $\mathcal{O}(n\log n)$，但需要额外的存储空间。  
* 快速排序的效率为 $\mathcal{O}(n\log n)$，但如果拆分点并不靠近列表的中间会变差为 $\mathcal{O}(n^2)$ 。此外其无需额外存储空间。


```python

```
