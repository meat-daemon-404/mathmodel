# MathModel (`zcode-mathmodel` v1.1.0)

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Python 3.10+](https://img.shields.io/badge/Python-3.10%2B-3776AB?logo=python&logoColor=white)](https://github.com/meat-daemon-404/mathmodel)
[![Tests](https://img.shields.io/badge/Verification-6_Test_Suites_Passing-2ea44f)](https://github.com/meat-daemon-404/mathmodel/tree/main/tests)

[English](README.md) | [简体中文](README.zh-CN.md)

> **面向全国大学生数学建模竞赛（国赛 CUMCM / 美赛 MCM-ICM）的 ZCode 自主数模智能体与 MCP 引擎** —— 提供 `mathmodel@mathmodel` 与 `mathmodel@inline` 双智能体入口，内置持久化 Python 科学计算内核、免 SciPy 便携数模算法库、灵敏度分析与论文图表流水线，以及确定性爆炸半径安全门禁。

## 双智能体入口与 MCP 工具清单

### 智能体角色（`plugin.json`）
- **`mathmodel@mathmodel`**：全流程自主数学建模主智能体，负责问题拆解、数据清洗、模型求解、图表绘制、灵敏度检验与国赛/美赛论文排版。
- **`mathmodel@inline`**：编辑器内联轻量助手，用于公式推导、局部代码片段验算与数据表快速诊断。

### 核心 MCP 工具（`engine/mcp_server.py`）

| 工具名称 | 功能说明 |
| :--- | :--- |
| `mcp__plugin_mathmodel_mathmodel-engine__run_task` | 执行多步自主数学建模子任务，自动记录中间图表、数据表与回滚快照 |
| `mcp__plugin_mathmodel_mathmodel-engine__run_python` | 在持久化 Python 科学计算内核中执行代码并保留上下文变量与异常堆栈 |
| `mcp__plugin_mathmodel_mathmodel-engine__blast_radius` | 在代码或命令执行前进行确定性爆炸半径审计，拦截越界写盘与破坏性指令 |
| `mcp__plugin_mathmodel_mathmodel-engine__list_models` | 查询当前配置的 LLM 模型端点、权重与故障转移状态 |

## 安全边界与便携性承诺

- **确定性安全红线**：高自由度代码执行**不等于**无边界系统修改。所有执行请求均受工作区沙箱与 `mcp__plugin_mathmodel_mathmodel-engine__blast_radius` 硬规则约束，任何提示词均**不能声称能绕过**路径越界拦截、破坏性命令阻断与密钥脱敏门禁。
- **免 SciPy 纯 NumPy 算法实现（`engine/tools_modelling.py`）**：内置 TOPSIS、层次分析法（AHP）、灰色预测 GM(1,1)、微分方程 RK4、线性规划单纯形法与蒙特卡洛模拟的纯 NumPy 实现，并通过 `tests/check_no_scipy.py` 强制校验。

## 快速开始与测试门禁

```bash
git clone https://github.com/meat-daemon-404/mathmodel.git
cd mathmodel
python -m pip install -e .

# 运行全套契约、工具与安全门禁测试
python -m unittest discover -s tests -p "test_*.py"
python tests/check_no_scipy.py
python tests/check_secrets.py
```

## 许可证

本项目基于 [MIT License](LICENSE) 开源。
