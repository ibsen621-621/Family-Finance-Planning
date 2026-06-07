# 🏠 家庭财务管理系统 (Family Finance Planning)

> 一套面向家庭的财务分析「代码指令集」，帮助你系统化地盘点收入、资产负债与投资组合，自动生成**月度财务复盘报告**，量化**财务健康度**，并跟踪你的 **FIRE（财务自由，提前退休）进度**。

---

## ✨ 功能总览

| 指令 | 作用 |
| --- | --- |
| `income` | 每月**收入分析**（主动/被动收入、来源构成） |
| `expense` | 每月**支出分析**（按类别拆解） |
| `balance` | **资产负债表**（总资产、总负债、净资产、负债率） |
| `portfolio` | **投资组合盘点**（资产配置、持仓盈亏、收益率） |
| `health` | **财务健康度评分**（0–100 分，四大维度） |
| `fire` | **FIRE 测算**（财务自由目标数字、进度、预计年限） |
| `report` | 一键生成 **月度家庭财务复盘报告**（Markdown） |
| `all` | 运行以上全部分析 |

---

## 📁 目录结构

```
Family-Finance-Planning/
├── README.md                 # 使用说明
├── requirements.txt          # Python 依赖
├── main.py                   # 命令行入口（指令集）
├── config/
│   └── settings.yaml         # 目标与参数配置（FIRE、储蓄率目标等）
├── data/                     # 你的财务数据（按月录入，可直接用 Excel 打开编辑）
│   ├── income.csv            # 收入
│   ├── expenses.csv          # 支出
│   ├── assets.csv            # 资产
│   ├── liabilities.csv       # 负债
│   └── investments.csv       # 投资组合
├── src/                      # 分析模块
│   ├── income_analysis.py    # 收入分析
│   ├── balance_sheet.py      # 资产负债
│   ├── portfolio.py          # 投资组合
│   ├── health_score.py       # 财务健康度
│   ├── fire_calculator.py    # FIRE 测算
│   └── monthly_report.py     # 月度报告生成
└── reports/                  # 自动生成的复盘报告输出目录
```

---

## 🚀 快速开始

### 1. 安装依赖

```bash
pip install -r requirements.txt
```

### 2. 运行示例（仓库已内置 2026-01 / 2026-02 两个月的示例数据）

```bash
python main.py all            # 运行全部分析并生成报告
python main.py report         # 仅生成月度复盘报告
python main.py fire           # 仅看 FIRE 进度
python main.py health --month 2026-01   # 指定月份
```

生成的报告会保存在 `reports/report-2026-02.md`。

### 3. 录入你自己的数据

用 Excel / 文本编辑器打开 `data/` 下的 CSV 文件，按既有格式逐月填写即可（删除示例行，换成你的真实数据）。

---

## 📝 数据录入说明

**`data/income.csv` — 收入**

| 字段 | 说明 | 示例 |
| --- | --- | --- |
| month | 月份 | 2026-01 |
| category | 收入类别 | 工资 / 副业 / 投资 |
| source | 具体来源 | 本人主业 / 股息分红 |
| amount | 金额 | 30000 |
| type | `active`（主动）或 `passive`（被动） | active |

**`data/expenses.csv` — 支出**：`month, category, description, amount`

**`data/assets.csv` — 资产**：`month, category, name, value, liquid`（`liquid` 填 `yes`/`no`，用于区分流动性资产与自住房等非流动资产）

**`data/liabilities.csv` — 负债**：`month, category, name, balance, interest_rate, monthly_payment`

**`data/investments.csv` — 投资组合**：`month, asset_class, name, value, cost_basis`

---

## 📊 核心指标说明

- **储蓄率** = （收入 − 支出）/ 收入。FIRE 追求者通常目标 ≥ 50%。
- **净资产** = 总资产 − 总负债。
- **应急基金覆盖月数** = 流动性资产 / 月支出，建议 ≥ 6 个月。
- **资产负债率** = 总负债 / 总资产，建议 ≤ 50%。
- **被动收入覆盖率** = 被动收入 / 支出，达到 100% 即意味着「财务自由」。
- **FIRE 数字** = 年支出 ÷ 安全提取率（默认 4%，即 **25 倍年支出**）。
- **FIRE 进度** = 当前可投资资产 / FIRE 数字。

> 财务健康度评分由「储蓄率 / 应急基金 / 负债率 / 被动收入」四个维度各 25 分组成，满分 100。

---

## 🔁 建议的使用节奏

1. **每月初**：更新上月的 `income` / `expenses`，并对 `assets` / `liabilities` / `investments` 做一次月末快照。
2. 运行 `python main.py report` 生成当月复盘报告。
3. 阅读报告中的「行动建议」，针对薄弱维度（如储蓄率、应急金）制定下月改进计划。
4. **每季度 / 每年**：回看 `reports/` 中历史报告，观察净资产与 FIRE 进度曲线。

---

## ⚙️ 个性化配置

编辑 `config/settings.yaml` 可调整：安全提取率、预期投资回报率、通胀率、目标储蓄率、应急基金月数、负债率警戒线、货币符号等。

---

> 💡 本项目所有计算均在本地完成，数据不外传。指标与建议仅供参考，不构成投资建议。祝早日实现 FIRE！
