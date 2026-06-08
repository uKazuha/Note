# 1. openpyxl模块

## 1.1 下载

```
pip install openpyxl
```

## 1.2 工作薄、工作表的连接建立

```python
from openpyxl import Workbook
from openpyxl import load_workbook

# 创建工作蒲
wb = Workbook()
# 创建工作表
ws = wb.active()
ws.title = "测试1"
wb.save("测试1.xlsx")
wb.close()

# 访问已有工作薄的工作表
wb = load_workbook(filepath)
ws = wb["sheetname"]

# 访问工作表的单元格
cell_range = ws["A1:D5"]	
cell = ws["A1"]
cell = ws[row=row,col=col]

# 访问单元格的内容,注意，如果单元格里的值是公式生成的，那么读取时的内容是公式，要实际值的话在打开工作薄是，设置参数wb=load_workbook(filepath,data_only=True)
val = cell.value
```

## 1.3 增删改查

```python

```



