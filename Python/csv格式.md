# csv格式

CSV = Comma-Separated Values

就是逗号分隔值文件，是一种纯文本格式，用来存储表格数据，用逗号把每一列分开，换行代表一行

注意：大多数都是逗号作为分隔符，也有些用分号

如下：

```
张三,18,男
李四,19,女
王五,20,男
```



csv里两个重要的对象：writer和reader

首先是writer对象：

```python
import csv

# 写入数据
data = [
    ["姓名", "年龄", "城市"],
    ["张三", 22, "东莞"],
    ["李四", 25, "武汉"],
    ["王五", 30, "苏州"]
]

with open("test.csv", "w", encoding="utf-8", newline="") as f:
    writer = csv.writer(f)
    writer.writerows(data)  # 一次性写入多行
    # writer.writerow(["赵六", 28, "黄石"])  # 写入单行

    #newline=""，这一步是在windows下必须的，这可以避免多余的空白行
```

在使用writer对象进行对csv文件写数据时：

首先时打开文件操作获取文件句柄fp，通过csv.writer类传进取实例化一个writer对象

再使用writer对象的方法进行数据的写入，有writerrow写一行还有writerrows写多行

在文件open时可以设置参数，即文件的写入格式

在获取writer对象时，设置参数，可以指定分隔符识别，默认逗号





其次是reader对象

```python
import csv

with open("test.csv", "r", encoding="utf-8") as f:
    reader = csv.reader(f)
    for row in reader:
        print(row)
```

