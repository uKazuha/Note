# 1. openpyxl模块

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

