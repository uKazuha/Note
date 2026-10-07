# 1.PYTHON基础

## 第1章  变量和简单数据类型

### 1.变量：一个记号，用来代表某个数据

* 命名规则：只能包含字母、数字或下划线，不能以数字开头，不能有空格或者以关键字为名

  可以使用以下方式来查看有哪些关键字

  ```python
  import keyword
  print(keyword.kwlist)
  ```

  

### 2.简单数据类型

* 字符串：用单引号或者双引号括起来的内容，单双引号配合使用可使字符串里包含引号

```
字符串的操作：
	+、title、upper、lower、strip、rstrip、lstrip
以上包括连接字符串、取大小写、去空白、使字符串以标题格式表现等操作
```

* 数字

  * 整数：+、-、*、/、%、**

    两个数都是整数之间的运算

  * 浮点数：有小数参与运算的情况，结果包含的小数位数可能是不确定的，所有语言都有这个问题，这和计算机底层存储方式有关，具体可学习计算机组成原理时了解

* 数字和字符串的转换

```
str(数)：可转换成字符串类型
int(字符串)：将只包含数字的字符串转换成整型
float(字符串)：将包含数字的字符串转换成浮点型
```

### 3.注释

使用 # 进行单行注释

使用'''  注释内容  '''进行多行注释



## 第2章 列表

```
列表[]

1.访问列表元素：
	索引访问[0]

2.修改列表元素
	索引定位赋值 lst[0] = 1
	
3.添加元素
	末尾添加：lst.append(value)
	插入：lst.insert(idx,value)

4.删除元素
	del lst[0]
	value = lst.pop()/lst.pop(idx)
	lst.remove(value)    注意，这样只能删除列表中第一个value（可能有多个相同的value）
	
5.排序
	lst.sort()	：永久排序，首字母
	sorted(lst)	：临时排序

6.倒置列表
	lst.reverse()
	
7.求列表长度
	len(lst)
	
8.列表解析
	lst = [value表达式 for value in 迭代式如range(1,10)]
	
9.切片
	lst[start:end:step]
	小tips：可以用lst[:]来快速复制一个列表	如new_lst = lst[:],如果只是简单赋值，则实际上是两个列表名指向同一个列表
```

## 第3章  元组

```
tup = (value)
元组中的元素不可重复，不可修改

误区：tup1 = (400,10)
	 tup1 = (10，20)
     上面这种是没问题的，这只是给元组变量赋值而已，不是修改元组

```

## 第4章  字典

```
字典：键值对
dic = {key:value}

1.访问字典值
	利用键名：dic[key]

2.添加键值对
	dic[key] = value
	
3.修改值
	dic[key] = value

4.删除键值对
	del dic[key]

5.遍历字典
	for key,value in dic.items()

6.遍历键、值
	for key in dic.keys()
	for value in dic.values()

7.嵌套
	在列表里存储字典
	在字典里存储列表
	在字典里存储字典
```



## 第5章  函数

### 1.定义函数

```python
def func(param):
    pass
```

函数名后面的括号里，包含着的是参数

参数有形参和实参的进一步细分，可以理解为定义函数时的param是一个占位的形参，而使用函数时，这个参数给的具体内容就是实参

### 2.传递实参

* 位置实参

```python
def func(p1,p2):
	pass

# 具体使用时
func("张三"，18)
# 此时，p1就是张三，p2就是18,调用时就是根据顺序位置，来把形参和实参连接起来
```

* 关键字实参

```python
def func(p1,p2):
	pass

# 具体使用时
func(p2="张三"，p1=18)
# 此时，p1就是18，p2就是张三，调用时，形参和实参不再根据顺序位置对应，而是使用者自己指定
```

* 默认值

```python
def func(p1,p2="张三"):
	pass

# 具体使用时
func(18)
# 此时，我们使用func时只传递了一个18，也可正常调用，这就好比调查问卷，有人不想实名制，我们就可以用一个代号张三来表示这个人
```

* 返回值

  函数是一个处理过程，这个过程可能有一个数据结果，这时可以通过返回值来表示

```python
def func():
    # 处理过程
    return result
```

### 3.传递列表

将列表传递给函数后，函数可对其修改，这个修改是**永久性**的

### 4.传递任意数量的实参

有时候你不清楚给一个函数设置多少形参才能满足所有需求，此时可以用以下方式实现

```python
def func(*param):
    pass

# 将形参名前用一个*号，代表创建一个名为param的空元组，传递实参时，解释器会把你传递的参数分装到这个元组里
```

有时不清楚形参的数量，更不清楚使用时，传递的这些参数是什么意思，此时可以通过允许传递任意数量的关键字实参

```python
def func(**param):
    pass

# 类似的，加两个*号代表创建一个名为param的空字典，后面的处理类似
```

### 5.将函数存储在模块中

* 导入模块
* 导入模块的某个函数
* 使用as给模块取别名
* 使用as给函数取别名



## 第6章  类

### 1.创建和使用类

```python
class ClassName(object):
	def __init__(self):
        pass
```

类中的函数称为方法，特殊的有一个__init__方法，括号里的self参数，每次根据类创建实例对象时，都会调用这个方法进行初始化

```python
# 创建实例
dog = Dog("papi"，3)

# 访问属性
name = dog.name

# 访问方法
dog.eat()
```

### 2.继承

有父类和子类的概念，在创建一个类的时候类名后的括号，就是本子类要继承的父类名

例如父类Car，子类Benzi

```python
class Car():
    def __init__(self,name):
        self.name = name
        
class Benzi(Car):
    def __init__(self,name,master):
        super().__init__(name)
        self.master = master
```



在使用子类实例化一个对象时，它是这样操作的：子类创建实例时，首先需要给父类的所有属性赋值（调用父类的init方法初始化）,利用super()，这里的super()其实就是父类

* 给子类定义属性和方法

父类的属性和方法被所有子类继承，而子类通常也会有属于自己的属性和方法

* 重写父类的方法

子类通常需要具体的操作

* 将实例用作属性

有时类不断增加细节后会显得很臃肿，这时就可以将一部分抽离出来定义一个新类，比如电动车有电池这个属性，但是对于电池来说，也有很多属于电池的细节

```python
self.battery = Battery()
```



## 第7章  文件和异常

### 1.从文件中读取数据

* 文件路径
* 打开与关闭文件

```python
fp = open(文件路径)
fp.close()


with open(文件路径) as fp:
    pass
```

* 逐行读取

```python
with open(文件路径) as fp:
    for line in fp:
        print(line)
```

* 读取的相关操作

```python
fp.read()
fp.readline()
fp.readlines()
fp.readable()
```



### 2. 写入文件

```
fp.write()
fp.writelines()
fp.writeable()
```

### 3.异常

* try-except-finally




