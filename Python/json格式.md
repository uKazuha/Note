# json模块

## 一、 json是什么？

json模块是用来处理json对象的，它是一种数据的存储格式

注意：json是文本字符串

语法规则：

* 整体用大括号 { } 包裹
* 内部是键值对：key:value，多个键值对使用逗号分开
* 键必须使用双引号
* 值支持以下几种类型：
  * 字符串
  * 数字
  * 布尔
  * 数组
  * 对象
  * null



**误区！**

语法规则里谈到的整体用大括号，内部是键值对并不绝对

因为json里有两个顶层格式，一种是如上所述，另一种是列表中括号，加列表元素的格式

也就是说：①大括号里面的是键值对，由字典转来

​					②中括号里面是列表元素，由列表转来



```json
{
  "name": "张三",
  "age": 22,
  "isStudent": true,
  "hobbies": ["篮球", "阅读"],
  "address": {
    "city": "东莞"
  },
  "remark": null
}
```

json数组：元素是json字符串的数组



## 二、 json模块的使用

### 1.dump和dumps

两者都是把Python对象（dict/list等）转为JSON格式

区别：

* dump：写入文件
* dumps：返回字符串



* json.dumps()

```python
import json

data = {"name":"张三", "age":20}
json_str = json.dumps(data, ensure_ascii=False, indent=2)
print(json_str)
print(type(json_str)) # <class 'str'>
```



* json.dump()

```python
import json

data = {"name":"张三", "age":20}
with open("test.json","w",encoding="utf-8") as f:
    json.dump(data, f, ensure_ascii=False, indent=2)
```



### 2.load和loads

两者都是把JSON格式转为Python对象（dict/list等）

区别：

* load：从文件中读取到Python对象
* loads：从JSON字符串中读取到Python对象



* json.load()

```python
import json

# 打开json文件，f是文件句柄
with open("data.json", "r", encoding="utf-8") as f:
    data = json.load(f)  # 传入文件对象fp
print(type(data)) # dict
```

* json.loads()

```python
import json

json_str = '{"name":"张三","age":20}'
data = json.loads(json_str) # 传入json字符串
print(type(data)) # dict
print(data["name"])
```





