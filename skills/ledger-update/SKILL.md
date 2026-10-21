---
name: ledger-update
description: 维护投递/面试台账（Excel）时使用：写前备份、按公司名动态定位、写后回读断言、禁止硬编码行号
---

# 台账安全更新

## 何时触发

- 新增岗位行、更新投递状态、记录 HR 回复、更新简历版本文件名

## 硬规则

1. **写前必先备份**：`<台账>_backup_<YYYY-MM-DD>.xlsx`，同日多份自动加 b/c/d…
2. **不用硬编码行号**：行数会因插入漂移。永远用「公司名」在 B 列定位，命中数必须 = 1，否则中止。
3. **写后回读**：重新打开工作簿读回该单元格，打印旧值/新值，确认落盘。
4. 插入新行前，先定位「用法」注记行，插在它前面；数据区末行 = 注记行 - 1（不写死）。

## 工具

`scripts/ledger.py`（python + openpyxl）：

```bash
python scripts/ledger.py backup
python scripts/ledger.py rows 关键词
python scripts/ledger.py set "公司关键词" N "新状态文本"
```

## 自检

- [ ] 备份文件已生成且时间戳为今天
- [ ] set 操作命中唯一行（输出里有公司名与行号）
- [ ] 回读值 = 期望值
- [ ] 新插的行没有把「用法」注记行挤乱
