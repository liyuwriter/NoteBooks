# Python笔记

## Python中的变量：



## Python中的数据类型：

**number（数值类型）**

- int（整数类型）

```python
a = 3
```

- float(浮点数类型)

```python
a = 2.44
```



**str（字符串类型）**

字符串：

有引号就是字符串，字符串有单引号，双引号，三引号，元字符串。

三种代表的字符串意义一样。

1. 单引号字符串：

```python
word = 'Hello Python!'
```

2. 双引号字符串：

```python
word = "Hello Python!"
```

3. 三引号字符串：

```python
"""
这里，
也是，
一个字符串
"""
# 三个字符串通常用来做模块、函数、包等多行注释。
# 也通常用于换行时候的字符串
```

4. 元字符串：

```python
word = r"c:\python\n"
print(word)
# 打印如下：
c:\python\n
# 元字符串会原封不动打印，但是有一点是最后一个字符不能是\字符
```

**特殊**：

双引号里面使用`\`+字母，来让无意义的字符变得有意义，或者让有意义的变得无意义，如下：

```python
# \+字符变得有意义：
\n # 换行
\r\n # 换行
\t # 制表符
\r # 将\r后面的字符串拉到当前行首

# 示例如下：

# \n的换行
word = "Hello,\nPython!"
print(word)
# 打印如下：
Hello,
Python!

# \r\n
word = "Hello,\r\nnPython!"
print(word)
# 打印如下：
Hello,
Python!

# \t制表符
word = "Hello,\tPython!"
print(word)
# 打印如下：
Hello,	Python!

# \+字符变得无意义：
word = "He sed \"this is a apple\""
print(word)
# 打印如下：
He sed "this is a apple"
```

**字符串的格式化**：

占位符：

`%d`：整形占位符

`%s`：字符串占位符

`%f`：浮点型占位符

```python
# %d占位符
word = "现在时间是下午%d点钟" % 1
print(word)
# 打印如下：
现在时间是下午1点钟

word = "现在时间是下午%2d点钟" % 1 # %2d表示占两位，不够拿空格来补位，字符串居右
print(word)
# 打印如下：
现在时间是下午 1点钟

word = "现在时间是下午 %-2d 点钟" % 1 # %-2d表示占两位，不够拿空格来补位，字符串居左
print(word)
# 打印如下：
现在时间是下午1 点钟

# %f浮点数占位符
word = "我今天花了%f元，买了%d个气球。" % (2.4, 1)
print(word)
# 打印如下：
我今天花了2.400000元，买了1个气球。

# %.2f浮点数占位符
word = "我今天花了%.2f元，买了%d个气球。" % (2.43, 1) # %f.2表示保留2位小数（存在四舍五入情况，默认保留6位小数）
print(word)
# 打印如下：
我今天花了2.43元，买了1个气球。

# %s字符占位
word = "%s，是我的好朋友。" %"小明"
print(word)
# 打印如下：
小明，是我的好朋友。

# 综合案例
# %s字符占位
word = "我是一名学生，我叫%s,我今年%d岁了，我身高有%.2f米" % ( "小红", 12, 1.68 )
print(word)
# 打印如下：
我是一名学生，我叫小红,我今年12岁了，我身高有1.68米
```

字符串的相关操作：

```python
# 字符串的拼接 +
strvar1= "hello"
starvar2 = "nihao"
print(strvar1 + starvar2)
# 打印如下：
hellonihao

# 字符串的重复
strvar1= "hello"
print(strvar1 * 3)
# 打印如下：
hellohellohello

# 字符串的拼接 \
var1 = "helol"\
"nihao"
print(var1)
# 打印如下：
helolnihao

# 字符串的索引
var = "nihao"
print(var[2])
# 打印如下：
h

# 字符串的切片
var = "nihao"
print(var[1:3])
# 打印如下：
ih

var = "nihao"
print(var[:3])
# 打印如下：
nih

var = "nihao"
print(var[2:])
# 打印如下：
hao

var = "nihao,你好"
print(var[-7:-5])
# 打印如下：
ih

var = "nihao,你好"
print(var[-5:-10:-2])
# 打印如下：
ai
```

**字符串的方法**

```python
# capitalize  首字母大写
str = 'hello,world'
res = str.capitalize()

# title 每个单词首字母大写
res = str.title()

# upper 将所有字母大写
res = str.upper()

# lower 所有字母变成小写
res = str.lower()

# swapcase 大小写互换
res = str.swapcase()

# len 计算字符串长度
res = str.len()

# count 统计字符串中某个元素的数量
res = str.count('a')

# find 查找某个字符串第一次出现的索引位置
# find(字符串,开始值,结束值)
res = str.find('w')

# index 与find功能相同，find找不到返回-1，index找不到直接报错
res = str.index()

# startswith 判断是否已某个字符或字符串开头
# startswith('字符串',开始值,结束值)
res = str.startwith('h')
res = str.startwith('h', 3, 6)

# endswith 判断是否以某个字符或字符串结尾
res = str.endswith('d')
# startswith('字符串',开始值,结束值)

# is系列：
# isupper 判断字符是否都是大写字母
# islower 判断字符是否都是小写字母

# isdecimal 判断字符串是否都是数字组成 必须是纯数字
str = '12344'
res = str.isdecimal()
True
str = '12.344'
res = str.isdecimal()
False

# 字符串中重要的方法
# split 按照某个字符串分割成列表
star = "hello,world"
res = star.split()

star = "hello#world#nihao#hello"
res = star.split('#')

# join 按某个字符将列表拼接成字符串（容器类型都可以）
lst = [ 'you', 'can', 'you', 'up', 'no', 'can', 'no', 'bb']
str = ' '.join(lst)
str = '#'.join(lst)

# replace 把字符串中旧字符替换新字符
# 'asdfsdf'.replace('d', 'D', 1)
str = "hello,world"
res = str.replace('l', 'L', 2)

# strip 默认去掉首位两边的空白符
str = ' hello,world '
res = str.strip()

# center 填充字符串，源字符串居中
str = 'nihao'
res = str.center(10, '*')

```





**list（列表）**

定义一个普通的列表：

```python
list_var = [1, 2, 3, 4]
print(list_var)
# 打印如下：
[1, 2, 3, 4]

list_var = [1.56, "hello", True, 88]
print(list_var)
# 打印如下：
[1.56, 'hello', True, 88]
```

获取列表里面的元素：

```python
list_var = [1.56, "hello", True, 88]
print(list_var[0])
# 打印如下：
1.56

list_var = [1.56, "hello", True, 88]
print(list_var[2])
# 打印如下：
True

list_var = [1.56, "hello", True, 88]
print(list_var[-2])
# 打印如下：
True
```

通过下标操作列表：

```python
# 通过下标获取值
listvar = ["a", 1, "time", 5]
print(listvar[2])
# 打印如下：
time

# 通过下标修改值
listvar = ["a", 1, "time", 5]
listvar[2] = "小明"
print(listvar)
# 打印如下：
['a', 1, '小明', 5]

# 通过负索引获取值，负索引是从右往左，第一个下标是-1
listvar = ["a", 1, "time", 5]
print(listvar[-1])
# 打印如下：
5

# 更多序列切片的例子
listvar = ["a", 1, "time", 5, "Hello", "A", 90]
print(listvar[-4:])
print(listvar[2:3])
print(listvar[:])
print(listvar[0:4:2])
# 打印如下：
[5, 'Hello', 'A', 90]
['time']
['a', 1, 'time', 5, 'Hello', 'A', 90]
['a', 'time']

# 列表拼接
list1 = ["a", "b"]
list2 = ['c', 'd']
res = list1 +list2
```

列表的方法：

**增加**

```python
# 增加
# append 从列表后面添加新的元素
listvar1 = [1, 2, 4]
listvar1.append(6)
print(listvar1)
# 打印如下：
[1, 2, 4, 6]

# insert 在指定的索引之前插入元素
str = ['a','b']
str.insert(0, "c")

# extend 迭代追加所有元素,要求追加的是一个可迭代数据（容器类型，range对象，迭代器）
lst = ["a", "b", "c"]
tup = (1, 2, 3)
lst.extend(tup)
# ["a", "b", "c", 1, 2, 3]
```

**删除**

```python
# 删除
# pop 指定索引删除元素，若没有索引，则移除最后的元素，并将删除的数据返回
lst = ["a", "b", "c"]
res = lst.pop()
# ["a", "b"]
lst = ["a", "b", "c"]
res = lst.pop(1)
# ["a", "c"]

# remove 删除某个具体的元素,多个相同的元素则删除第一个出现的
lst = ["a", "b", "c", "b", "c"]
lst.remove("b")
["a", "c", "b", "c"]

# clear 清空列表
lst = ["a", "b", "c", "b", "c"]
lst.clear()
```

**其他**

```python
# index获取某个值在列表中的索引
lst = ["a", "b", "c", "b", "c"]
res = lst.index('c')
res = lst.index('c', 3)
res = lst.index('c', 0, 3)

# count 获取某个值在列表中出现的次数
lst = ["a", "b", "c", "b", "c"]
res = lst.count('c')

# sort 对列表进行排序
lst = [-99, 100, -1]
lst.sort() # 从小到大
lst.sort(reverse=True) # 从大到小

lst = ['a', 'ab', 'ac']
lst.sort() # 根据ASCII码排序

# reverse 列表反转
lst = ['a', 'ab', 'ac']
lst.reverse()
# ['ac', 'ab', 'a']
```

**列表的拷贝**

1. 浅拷贝
2. 深拷贝

浅拷贝：变量重定向到其他数据

```python
# 将数组拷贝到另一个副本,浅拷贝
import copy
lst1 = ['a', 'b', 'c', 'd']
lst2 = copy.copy(lst)
lst1.append(10)
# lst1  ['a', 'b', 'c', 'd', 10]
# lst2  ['a', 'b', 'c', 'd']

# 方法2
lst2 = lst1.copy()
lst1.append(1)
# lst1 ['a', 'b', 'c', 'd', 1]
# lst2  ['a', 'b', 'c', 'd']

# 浅拷贝遇到的特点，只将一级容器里面的数据拷贝
lst1 = [1, 3, 4, [7, 8, 0]]
lst2 = copy.copy(lst1)
lst1[-1].append(9)
# list1 [1, 3, 4, [7, 8, 0, 9]]
# list2 [1, 3, 4, [7, 8, 0, 9]]
```

深拷贝：变量指定源数据

```python
import copy
lst1 = [1, 3, 4, [7, 8, 0]]
lst2 = copy.deepcopy(lst1)
lst1[-1].append(9)
# list1 [1, 3, 4, [7, 8, 0, 9]]
# ist2 [1, 3, 4, [7, 8, 0]
```



**dir（字典）**

字典的定义：

```python
dirvar = {"name": "xiaowang", "age": 15}
print(dirvar)
print(type(dirvar))
# 打印如下：
{'name': 'xiaowang', 'age': 15}
<class 'dict'>

# 定义空字典
dictvar = {}
```

通过键获取值：

```python
dirvar = {"name": "xiaowang", "age": 15}
print(dirvar["name"])
# 打印如下：
xiaoming
```

通过键改变值：

```python
dirvar = {"name": "xiaowang", "age": 15}
dirvar["name"] = "laowang"
print(dirvar["name"])
# 打印如下：
laowang
```

字典要注意的是，有些数据类型不能做键，所以类型都可以做值，可以做键的是“不可变”类型，或者说可以hash的都可以作为集合的值和字典的键，如下：

1. Number
2. str
3. tuple

从这里可以看出来，字典和集合都是无序的（表面有序，实际无序），因为他们都使用了hash算法存储数据的原因。

在python3.6版本后对字典排序做了优化，看起来是有序的，但底层还是无序。

**字典的方法：**

```python
dic = {"name": "xiaohu", "age": 16}
print(dic)
# 打印如下：
{'name': 'xiaohu', 'age': 16}

# fromkeys 使用一组键和默认的值创建字典
# fromkeys("容器", "默认值")
tup = ("a", "b", "c")
dic = {}.fromkeys(tup, None)
print(dic)
# 打印如下：
{'a': None, 'b': None, 'c': None}

tup = ("a", "b", "c")
dic = {}.fromkeys(tup, [])
print(dic)
# 
{'a': [], 'b': [], 'c': []}

tup = ("a", "b", "c")
dic = {}.fromkeys(tup, [])
dic["a"].append(2)
print(dic)
# 
{'a': [2], 'b': [2], 'c': [2]} # 可以看出来a, b, c默认指向一个列表

# 字典删除 pop
dic = {"name": "xiaohu", "age": 16, "school": "ust"}
res = dic.pop("age")
print(res)
print(dic)
# 打印如下：
16
{'name': 'xiaohu', 'school': 'ust'}

dic = {"name": "xiaohu", "age": 16, "school": "ust"}
res = dic.pop("ag", "该值不存在")
print(res)
print(dic)
# 
该值不存在
{'name': 'xiaohu', 'age': 16, 'school': 'ust'}

# popitem()，删除最后一个键值对
dic = {"name": "xiaohu", "age": 16, "school": "ust"}
res = dic.popitem()
print(res)
print(dic)
# 打印如下：
('school', 'ust')
{'name': 'xiaohu', 'age': 16}

# clear()清空字典
dic = {"name": "xiaohu", "age": 16, "school": "ust"}
dic.clear()
print(dic)
{}

# 字典的更改
# update()，批量更新，如果有键则更新，没键就增加
dic_new = {"test": "top"}
dic = {"name": "xiaohu", "age": 16, "school": "ust"}
dic.update(dic_new)
print(dic)
# 打印如下：
{'name': 'xiaohu', 'age': 16, 'school': 'ust', 'test': 'top'}

# 有值就更新
dic_new = {"school": "WTS"}
dic = {"name": "xiaohu", "age": 16, "school": "ust"}
dic.update(dic_new)
print(dic)
# 打印如下：
{'name': 'xiaohu', 'age': 16, 'school': 'WTS'}

# 查，get()即使没有对应的键，也不会报错，会返回None，还可以自定义值
dic = {"name": "xiaohu", "age": 16, "school": "ust"}
res = dic.get("name")
res1 = dic.get("Test")
res2 = dic.get("Test","该值不存在")
print(res)
print(res1)
print(res2)
# 打印如下：
xiaohu
None
该值不存在

# 其他操作
# keys()，将字典的键值组成新的可迭代对象
dic = {"name": "xiaohu", "age": 16, "school": "ust"}
res = dic.keys()
for i in res:
    print(i)
# 打印如下：
dict_keys(['name', 'age', 'school']) # 这个数据类型是dict_keys，一种不标准的数据类型，可迭代对象
name
age
school

# item()方法，将字典的键值对变成一个个元组，组成新的可迭代对象
dic = {"name": "xiaohu", "age": 16, "school": "ust"}
res = dic.items()
print(res)
# 打印如下：
dict_items([('name', 'xiaohu'), ('age', 16), ('school', 'ust')])

# 将字典转为可迭代对象后获取
dic = {"name": "xiaohu", "age": 16, "school": "ust"}
res = dic.items()
for k, v in res:
    print(k, v)
#打印如下：
name xiaohu
age 16
school ust
```





**集合（set）**

集合是无序的，且自动去重，所以集合一般用来做交叉并补。

因为集合是无序的，所以不能通过下标来操作。

```python
setvar = {"Hello", "Hi", 3, 5, 99, "Hello"}
print(setvar)
print(type(setvar))
# 打印如下：
{3, 99, 5, 'Hello', 'Hi'}
<class 'set'>
```

集合唯一不同的是，空集合定义与集合值的特定类型：

```python
setvar = set()
print(type(setvar))
# 打印如下：
<class 'set'>

# 集合中的值只能是不可变类型
# Number str tuple
```

**集合的方法**：

```python
# add 添加元素
set1 = {1, 2, 3}
set1.add(4)

# update 迭代增加
str = "aaa"
set1.update(str)

# pop 随机删除一个数据
p = set1.pop()

# discard 删除指定元素，不存在的不删除
set1.discard(1)

# remove 删除指定元素，不存在的不删除
set1.remove(1)

```



**元组**

元组是不可变类型：

```python
var = (1, 2, 3, 4)
print(var)
print(type(var))
# 打印如下：
(1, 2, 3, 4)
<class 'tuple'>

var = (1, 2, 3, 4)
var[1] = "a"
# 报错如下：
TypeError: 'tuple' object does not support item assignment

# 如果是一个数组，则也要写,
var = "a",
print(var)
print(type(var))
# 打印如下：
('a',)
<class 'tuple'>
```



**python中变量在内存的存储**：

**整数**：

> 在python3.6版本中，对于整数而言，-5~正无穷的范围内的相同值，则id一致。也就意味着这个范围内相同的值都是一个内存空间。

```python
var1 = 6
var2 = 6
print(id(var1), id(var2))
# 打印如下：
1600128680336 1600128680336
```

**浮点数**：

```python
var1 = -1.22
var2 = -1.22
print(id(var1), id(var2))
# 打印如下：
1643581137168 1643581137168


var1 = -1.22
var2 = -1.22
print(id(var1), id(var2))
# 打印如下：
2541004256048 2541004256048
```

**布尔值**：

> 对于布尔值而言，值相同的情况下，id一致

```python
var1 = True
var2 = True
print(id(var1), id(var2))
# 打印如下：
140731851664232 140731851664232

var1 = True
var2 = False
print(id(var1), id(var2))
# 打印如下：
140731851664232 140731851664264
```

**复数**：

> python3.6之前，复数在实数+虚数的结构中永不相同，只有在正5j情况下例外，目前python3.11都是一样。

```python
var1 = 6 + 7j
var2 = 6 + 7j
print(id(var1), id(var2))
# 打印如下：
2839417714192 2839417714192
```

**容器**：

> 在pyton3.6版本之前，字符串和空元组相同的情况下，id一致，其余情况都不一致
>
> 但是在之后的版本中，元组相同也一致

```python
var1 = "Hello"
var2 = "Hello"
print(id(var1), id(var2))
# 
2432287205680 2432287205680

var1 = ()
var2 = ()
print(id(var1), id(var2))
#
2158857044080 2158857044080

var1 = (1, 2)
var2 = (1, 2)
print(id(var1), id(var2))
#
2828587526080 2828587526080

# 列表则不同
var1 = [1, 2]
var2 = [1, 2]
print(id(var1), id(var2))
# 打印如下：
1554548321408 1554551486016
```



**python中的类型转换**

`int`强制把数据转为整型

```python
var1 = 11
var2 = 5.6
var3 = True
var4 = "1234"
var5 = "789ABC"

res = int(var2)
print(var2, type(var2))

res = int(var3)
print(var3, type(var3))

res = int(var4)
print(var4, type(var4))

res = int(var5) # 错误，因为不是纯数字的字符串转为int会失败
print(var5, type(var5))
# 打印如下：
5 <class 'int'>
1 <class 'int'>
1234 <class 'int'>
```

`float`强制转换为小数，可以将int，float，bool，纯数字字符串转换。

```python
var1 = 11
var2 = 5.6
var3 = True
var4 = "1234"
var5 = "789ABC"

res = float(var2)
print(res, type(res))

res = float(var3)
print(res, type(res))

res = float(var4)
print(res, type(res))

res = float(var5) # 错误
print(res, type(res))
# 
5.6 <class 'float'>
1.0 <class 'float'>
1234.0 <class 'float'>
```

`bool`将数据转换为布尔值

```python
# bool除了0，0.0，False，""，'',[],{},None,set() 转为False，其余都转为True
```

**自动转换**

python会将数据类型自动转换。

- 低精度默认向高精度转换

> bool  -> int -> float -> complex

```python
# bool + int
var1 = True + 1
print(var1)
#
2

# bool + float
var1 = True + 1.345
print(var1)
# 
2.3449999999999998

# bool+complex
var1 = True + 9j
print(var1)
#
(1+9j)

# int + float
var1 = 3 + 5.66
print(var1)
#
8.66

# 精度损耗
print(0.1 + 0.2 == 0.3)
print(1.5 + 1.5 == 3.0)
# 
False
True

# int + complex
res = 5 + 5 + 30j
print(res, type(res))
#
(10+30j) <class 'complex'>

# float + complex
res = 1.22 + 5.44 + 30j
print(res, type(res))
#
(6.66+30j) <class 'complex'>
```



## python中的运算符：

- 赋值运算符
- 成员运算符
- 算数运算符
- 比较运算符
- 身份运算符
- 位运算符



**成员运算符**：

```python
# 成员运算符：in和not in

container = [1, "ab", "B"]
res = "ab" in container
print(res)
# 打印如下：
True

container = [1, "ab", "B", 2]
res = "2" in container
print(res)
# 打印如下：
False

container = [1, "ab", "B", 2]
res = 2 in container
print(res)
# 打印如下：
True
```



**身份运算符**：

```python
# is 和 not （检测两个数据在内存中是否同一个值）
# 整数
var1 = 100
var2 = 100
print(var1 is var2)
# 打印如下：
True

# 负数
var1 = -10
var2 = -10
print(var1 is var2)


```



**逻辑运算符**：

```python
# 逻辑运算符： and or not
# and 逻辑与
res = True and True
print(res)
# 打印如下：
True

res = True and False
print(res)
# 打印如下：
False

# or逻辑或
res = True or True
print(res)
# 打印如下：
True

res = True or False
print(res)
# 打印如下：
True

res = False or False
print(res)
# 打印如下：
False

# not 逻辑非
res = not True
print(res)
# 打印如下：
False
```

**逻辑短路**：

当前面的逻辑直接决定结果后，后面的代码就不执行，例子如下：

```python
print(True or print("hello")) 
# 
True

False or print("hello")
#
hello
# 前面是正常的短路
```

还有一种是布尔值和表达式的短路：

```python
res = 3 and 2
print(res)
# 打印如下：
2

res = 3 or 2
print(res)
# 打印如下：
3

"""
计算规则:
	先计算当前表达式的布尔值是True还是False
	如果出现了True or 表达式 或者 False and 表达式的情况，直接返回前者，后面代码不执行
	如果没有出现短路情况，则返回后者
"""
```

逻辑运算符的优先级：

```python
() > not > and > or

res = 3 or 5 and 7
print(res)
# 打印如下：
3

res = (4 or 5) and 3
print(res)
# 
3

res = not (4 or 5) and 3
print(res)
# 
False

res = 1<2 or 3>4 and 5<100 or 100<200 and 700>800 or 1<-1
print(res)
#
True
```



**位运算符**：

```python
# 位运算符： & | ~ ^ << >>

# & 按位与
var1 =12
var2 = 23
res = var1 & var2
print(res)

# | 按位或

# ^ 按位异或
```



## python中的代码块

python中以冒号作为开始，以相同缩进来划分相同的作用域，这个整体是代码块。

python中的流程控制：

- 顺序结构（程序默认从上到下，依次执行）
- 选择结构
- 循环结构



**选择结构**：

```python
if 条件表达式:
    code1
    code2
# 当条件为True执行，否则不执行，例子如下：

# if else 语句，如果表达式为True则执行if代码块，否则执行else代码块
number = 10
if number <= 11:
    print("大与")
else:
    print("小于")
# 打印如下：
大于

if 条件表达式1:
     code1
elif 条件表达式2:
     code2
elif 条件表达式3:
     code3
else:
     code4        
```

**循环结构**：

循环结构在python中有几种关键词，如下：

- for
- while



```python
# 
number = 1
while number <= 10:
    print(number)
    number += 1
# 打印如下：
1
2
3
4
5
6
7
8
9
10

# for循环

for i in range(10):
    print(i)
# 打印如下：
0
1
2
3
4
5
6
7
8
9

# 一个有意思的输出
i = 1
flag = 0
while i <= 100:
    if flag % 2 == 0:
        print('*', end='')
    else:
        print('-', end='')
    if i % 10 == 0:
        flag += 1
        print()
    i += 1
# 打印如下：
**********
----------
**********
----------
**********
----------
**********
----------
**********
----------
```



## python中的文件操作:

文件的模式：

- w（write写入模式）
- r（read读取模式）
- a（append追加模式）
- x（xor异或模式）

扩展模式（配合打开模式的辅助模式，不能离开文件打开模式单独使用）

1. +（plus，增强模式，可以让文件具有读写功能）
2. b（bytes，bytes模式（二进制字节流））

文件的模式一共有16种：

w, w+, wb, wb+

r，r+，rb，rb+

a，a+，ab，ab+

x，x+，xb，xb+

```python
# 文件的写入
f = open("test.txt", mode="w", encoding="utf-8")
f.write("This is Test line")
f.close()

# 文件的读取
g = open("test.txt", mode="r", encoding="utf-8")
res = g.read()
g.close()
print(res)
# 打印如下：
This is Test line

# 字节流，用于传输数据或存储数据的一种格式，字节流模式不允许使用encoding

f = open("test.txt", mode="rb", encoding="utf-8")
res = f.read()
f.close()
print(res)

"""
二进制字节流，使用b开头，b"abc"，且只能是ascii码中的字符，不能是中文
将字符串和字节流类型进行转换
encode()编码，将字符串转化为字节流
decode()解码，将字节流转化为字符串
"""
data = b"abc"
print(date, type(data))
#
b'abc' <class 'bytes'>

data = "中文".encode("utf-8") # 编码
print(data, type(data))
#
b'\xe4\xb8\xad\xe6\x96\x87' <class 'bytes'>

res = data.decode("utf-8")
print(res)
# 打印如下：
中文

f = open("test.txt", mode="wb")
word = "你好".encode("utf-8")
f.write(word)
f.close()
# 文件内容如下：
你好


red = open("test.txt", mode="rb")
fs = red.read()
red.close()
print(fs)
# 打印如下：
b'\xe4\xbd\xa0\xe5\xa5\xbd'

# 二进制一般用来读取图片、视频，复制图片、视频等等操作
img = open("Zombatar_1.jpg", mode="rb")
red = img.read()
img.close()
new_img = open("1.jpg", mode="wb")
new_img.write(red)
new_img.close()

# read和w模式都是光标在文件开头
# a在文件末尾，可以使用seek方法将指针调整到文件开头
# seek(0) 把光标移动到0字节位置
# seek(0, 2)把光标移动到文件尾部
```



## python中的函数

python中函数使用`def`关键字来定义，因为python是属于解释型语言，所以再调用函数前，要先定义函数。

```python
def func(): # 定义一个函数，名称为func
    print("hello,world")

func() # 调用函数
# 打印如下：
hello,world
```

函数可以传递参数进去，其中在函数里面的参数称为形参，调用函数的时候传递的参数称为实参。

```python
def func(var):
    print(var)

func("你好")
# 打印如下：
你好
```

参数的传递有几种方法：

- 位置参数
- 关键字实参



收集形参：

- 普通收集形参 *args

```python
# *args 将多余的普通实参收集到一个元组中
def func(a, b, c, *args):
    print(a, b, c )
    print(args)

func(1, 2, 3, 4, 5)
# 打印如下：
1 2 3
(4, 5)

# 通过使用*agrs实现一个任意长度的计算器
def add(*args):
    var = 0
    for i in args:
        var += i
    print(var)

add(1, 2, 3, 5)
# 打印如下：
11
```



关键字收集形参 **args

```python
# **agrs将多余的关键字实参收集到一个字典中
def func(a, b, c, **args):
    print(a, b, c )
    print(args)

func(1, 2, 3, name='老刘', age='18')
# 打印如下：
1 2 3
{'name': 'T', 'age': '18'}
```



**函数的返回return**

```python
# 函数默认都有返回，None

def test():
    return "hello"
```



**函数的嵌套**



**全局变量与局部变量**





**闭包函数**

```python
# 闭包函数定义
# 1. 内嵌函数使用外部函数的变量
# 2. 外部函数直接返回内部函数
```



**lambda表达式**

lambda是python中的一种匿名函数，例如



**迭代器**





## python中的高阶函数

- map函数
- reduce函数
- filter函数
- sorted函数



```python
# filter函数
# 过滤数据，在自定义的函数中，如果返回True，该数据保留，如果返回False，该数据舍弃
# 

def func(n):
    if n% 2 ==0
      return True
    else:
        return False

lst = [1, 2, 3, 4, 5, 6, 7, 8, 9]
it = filter(func, lst)
print(list(it))
# 打印如下：
[2, 4, 6, 8]

# 使用lambda改写
lst = [1, 2, 3, 4, 5, 6, 7, 8, 9]
it = filter(lambda n: True if n% 2 ==0 else False, lst)
print(list(it))
# 打印如下：
[2, 4, 6, 8]
```



sorted函数：

```python
# sorted函数
# 对数据进行排序
# sorted（iterable，key=函数， reverse=False）
# iterable： 可迭代对象
# key：指定函数
# reverse： 是否倒叙
# 返回值：列表
tup = (1, 10, -90, 5)
res = sorted(tup)
print(res, type(res)) # 默认从小到大
# 打印如下：
[-90, 1, 5, 10] <class 'list'>

# 使用reverse指定从大到小
tup = (1, 10, -90, 5)
res = sorted(tup, reverse= True)
print(res, type(res))
# 打印如下：
[10, 5, 1, -90] <class 'list'>
```



## python中的推导式与生成器

**推导式**：

通过一行循环判断，遍历出一系列数据的方式是推导式。

语法：

```python
val for val in Iterable # 把想要的值写在for的左侧
# 推导式的三种：
# 

# 不用推导式时
lst = []
for i in range(1, 9):
    lst.append(i)
print(lst)

# 改写基本推导式
var = [ i*2 for i in range(1, 9) ]
print(var)

# 打印如下：
[1, 2, 3, 4, 5, 6, 7, 8]
[1, 2, 3, 4, 5, 6, 7, 8]

# [1, 2, 3, 4, 5] => [2, 4, 6, 8, 10]
var = [ i*2 for i in range(1, 6) ]
print(var)
# 打印如下：
[2, 4, 6, 8, 10]

# 带有判断条件的推导式，其中for后面的判断条件只能是单项分支
# [1, 2, 3, 4, 5, 6, 7, 8, 9, 10] => [1, 3, 5, 7, 9]
lst = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
var1 = [ i for i in lst if i % 2 ==1 ]
print(var1)
# 打印如下：
[1, 3, 5, 7, 9]

# 多循环的推导式
lst1 = [1, 2, 3, 4, 5]
lst2 = [10, 9, 8, 7, 6]
var1 = [i*j for i in lst1 for j in lst2]
print(var1)
# 打印如下：
[10, 9, 8, 7, 6, 20, 18, 16, 14, 12, 30, 27, 24, 21, 18, 40, 36, 32, 28, 24, 50, 45, 40, 35, 30]

# 带有判断条件的多循环推导式
# 多循环的推导式
lst1 = [1, 2, 3, 4, 5]
lst2 = [10, 9, 8, 7, 6]
var1 = [i*j for i in lst1 for j in lst2 if lst1.index(i) == lst2.index(j)]
print(var1)
# 打印如下：
[10, 18, 24, 28, 30]

# 变大写为小写
lst = ['A', 'B', 'C']
var = [i.lower() for i in lst ]
print(var)
# 打印如下：
['a', 'b', 'c']

# 生成元组
lst = [(i, j) for i in range(3) for j in range(3)]
print(lst)
# 打印如下：
[(0, 0), (0, 1), (0, 2), (1, 0), (1, 1), (1, 2), (2, 0), (2, 1), (2, 2)]
```

**生成器**：

生成器本质上是迭代器，允许自定义逻辑的迭代器。

迭代器和生成器的区别：

1. 迭代器本身是系统内置的，重写不了。
2. 生成器是用户自定义，可以重新和迭代

生成器可以用两种方式创建：

1. 生成器表达式（里面是推导式，外面用圆括号）
2. 生成器函数（用def定义，里面含有yield）

生成器表达式：

```python
# 生成器表达式
res = (i for i in range(5))
print(res)
# 打印为对象
<generator object <genexpr> at 0x00000128BF4D94A0>

# 判断是否为生成器
from collections import Iterable,Iterator 
print(isinstance(gen, Iterator))
# 打印如下：
True

# 生成器使用next调用
gen = (i for i in range(5))
print(next(gen))
print(next(gen))
# 打印如下：
0
1
```

生成器函数：

生成器函数有yield，类似于return，共同点在于执行到这段代码后都会u把值返回出去，不同点是yield每次返回时，会记住上次离开时执行的位置，下次调用生成器后，继续执行。而return则会终止函数，每次都从头调用。

```python
def func():
    print("111")
    yield 1

    print("222")
    yield 2

    print("333")
    yield 3

# 初始化生成器函数，返回生成器对象
gen =  func()
res = next(gen)
print(res)
# 打印如下：
111
1
# 第一次调用打印111，返回yield1，保存当前行代码状态，返回1，并且等待下一次调用

# 优化生成器代码
# 生成器应用的场景实在大数据的范围内使用，切记不可直接使用for遍历所有，可能无法短时间内获取所有数据
def mygen():
    for i in range(1,101):
        yield i

gen = mygen() # 获取生成器
for i in range(30):
    print(next(gen))
# 打印如下：
1
2
...
30


# send使用方式（给上一个yield发送数据）
# next和send的区别：
# next只能取值
# send能取值也能发
# send注意点：第一个send不能给yield传值，默认只能写None；最后一个yield接受不到send发送值
def mygen():

    print("start")

    res = yield "内部1"
    print(res, "<===内部===>")

    res = yield "内部2"
    print(res, "<===内部===>")

    res = yield "内部3"
    print(res, "<===内部===>")

# 初始化生成器，返回生成器对象
gen = mygen()

# 第一次调用发送None，前面介绍了第一个send不能给yield传值
res = gen.send(None)
print(res, "<===外部===>")

# 第二次调用生成器
res = gen.send("100")
print(res, "<===外部===>")

# 第三次调用生成器
res = gen.send("200")
print(res, "<===外部===>")

# 打印如下：
start
内部1 <===外部===> # 第一次调用，碰到yield后返回值为“内部1”，给生成器外部的res
100 <===内部===> # 第二次调用，将100传递给生成器的第一个yield，所以会打印“100 <==内部==>”，程序碰到第二个yield，将“内部2“返回给生成器外部的res，所以打印”内部2 <===外部===>”
内部2 <===外部===>
200 <===内部===> # 同理
内部3 <===外部===>
```



## python中的递归函数

递归函数，自己调用自己的函数。

每次调用一次函数，都会在内存中开辟一个空间，用来存放函数的变量等，这是栈帧空间。

```python
def func(n):
    print(n, "<===1===>")
    if n > 0:
        func(n-1)
    print(n, '<===2===>')


func(5)
# 打印如下：
5 <===1===>
4 <===1===>
3 <===1===>
2 <===1===>
1 <===1===>
0 <===1===>
0 <===2===>
1 <===2===>
2 <===2===>
3 <===2===>
4 <===2===>
5 <===2===>
```



## python中的内置函数

- abs 绝对值
- round  四舍五入，奇进偶不进
- sum 计算一个序列得和



## python中的模块

使用import导入模块

 **math**模块



**random**模块



**pickle**模块

序列化模块

把不能够直接存储在文件中的数据变得可存储

pickle模块有几个重要的方法

dumps：把任意对象序列化成一个bytes

```python
lst = [1, 3, 4, 6]
res = pickle.dumps(lst)
print(res, type(res))
# 
b'\x80\x04\x95\r\x00\x00\x00\x00\x00\x00\x00]\x94(K\x01K\x03K\x04K\x06e.' <class 'bytes'>
```

loads：把任意bytes反序列化成为原来的数据

```python
res2 = pickle.loads(res)
print(res2, type(res2))
```

dump：把对象序列化写入到file-like object（文件对象）



load：把文件对象内容拿出来，反序列化成为原来数据



**json**模块：

json模块也是序列化和反序列化模块，他和pickle的区别在于：

json注意应用与传输数据，序列化成字符串。

pickle用于存储数据，序列化成二进制字节流。

json格式的数据，所有编程语言都能识别，它本身是字符串。

```python
import json
dic = {"name": "小红", "age": 30}
res = json.dumps(dic)
print(res, type(res))
# 
{"name": "\u5c0f\u7ea2", "age": 30} <class 'str'>

# ensure_ascii=False，显示中文
import json
dic = {"name": "小红", "age": 30}
res = json.dumps(dic, ensure_ascii=False)
print(res, type(res))
# {"name": "小红", "age": 30} <class 'str'>

# sort_keys=True 按键排序
import json
dic = {"name": "小红", "age": 30}
res = json.dumps(dic, ensure_ascii=False, sort_keys=True)
print(res, type(res))
#
{"age": 30, "name": "小红"} <class 'str'>


import json
dic = {"name": "小红", "age": 30}
res = json.dumps(dic, ensure_ascii=False, sort_keys=True)
print(res, type(res))

dic = json.loads(res)
print(dic, type(dic))
#
{"age": 30, "name": "小红"} <class 'str'>
{'age': 30, 'name': '小红'} <class 'dict'>


```



## python中的魔术方法

```python
# __new__()方法
# __init__()方法
# __str__()方法
# __del__()方法
# __call__()方法
# __
```



## python中的类魔术属性

```python
# __dict__
# __doc__
# __name__
# __class__
# __bases__
```



## python中的异常处理

程序错误分为了两种：

1. 语法错误
2. 异常错误

python中的异常处理语法如下：

```python
try:
    ...
except: 
    ...
```

python中的异常分类如下：

```python
IndexError # 索引超出序列范围
KeyError # 字典中查找一个不存在的关键字
NameError # 访问一个不存在的变量
IndentationError # 缩进错误
AttributeError # 未知对象属性
StopIteration # 迭代器没有更多的值
AssertionError # 断言语句失败
EOFError # 用户输入文件末尾标志EOF(ctrl+d)
FloatingPointError # 
GeneratorExit #
ImportError # 导入出错
KeyboardInterrupt # 
OSEroor # 操作系统报错，一般打开不存在的文件等
OverFlowError #
ReferenceError #
RuntimeEroor #
StntaxError #
TabError #
SystemError #
SystemExit #
TypeError # 类型错误
UnboundLocalError #
UnicodeError #
UnicodeEncodeError #
UnicodeDecodeError #
UnicodeTranslateError #
ValueError # 无效参数
ZeroDivisionError # 除数为零 
```

python异常处理：

```python
# try except

try:
    fp = open("a.txt")
except OSError :
    print("打开不存在的文件")
# 打印如下：
打开不存在的文件
```

































