# 1.PYTHON基础

## 第1章  变量和简单数据类型

```
字符串的操作：
	+、title、upper、lower、strip、rstrip、lstrip
	单双引号的配合使用
```



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
	lst.sort()		：永久排序，首字母
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

```
def function(parameter1、2、...):
形参和实参
位置实参和关键字实参
默认值：def function(para1 = value, para2)

传递任意数量的实参
def func(*para)
以上的含义：预先创建一个名为para的空元组，然后接收实际传入的参数，最后将这个元组放入函数内使用
func(para1)
func(para1,para2,para3)


还有一种是
def func(para1,para2,**para)
以上的用法：func(para1,para2,key1=value1,key2=value2..)
```



## 第6章  类

```
class ClassName(object):
```











# 2.openpyxl模块

## 1.1 下载

```
pip install openpyxl
```

## 1.2 创建一个工作薄并插入数据

```python
from openpyxl import Workbook

# 创建工作蒲
wb = Workbook()
# 创建工作表
ws = wb.active()
ws.title = "测试1"

ws["A1"] = "123"

wb.save("测试1.xlsx")
wb.close()

```

## 1.3 读取一个工作蒲并插入数据

