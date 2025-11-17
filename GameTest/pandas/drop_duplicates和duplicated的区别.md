# 去重和找重复行的区别
## 只根据“患者ID”列去重（相同ID的行视为重复）

```python
data.drop_duplicates(subset=['患者ID'], inplace=True)
```

## 检测重复行

```python
duplicates = data.duplicated()
```