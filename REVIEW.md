# 审查建议

这个仓库可以作为第一轮探索实验，但在把结果视为可复现实验前，建议先修正下面几个问题。

## 高优先级

- 将数据库连接信息移出 `single_stock.ipynb`。当前 Notebook 的连接单元里直接写了 host、user、password 和 database，建议改为从 `.env` 环境变量读取。
- 移除 `/Users/hanxi/...` 这类本机绝对路径。Qlib 导出和 provider 路径建议使用仓库相对路径（如 `raw_data/`、`qlib_data/`）或环境变量，否则其他机器无法直接运行。
- Ridge 验证循环前需要导入 `mean_squared_error`。当前代码调用了该函数，但 import 被注释掉了。
- 修正 LightGBM 特征重要性单元。当前使用 `model.feature_importance(...)`，但 `model` 是 alpha 搜索循环里最后一个 Ridge 模型；这里应使用 `lgb_model.feature_importance(...)`。

## 方法论建议

- 增加“预测收益率恒为 0”的简单基线，并报告每个模型在 MSE、MAE 上是否超过该基线。
- 时间序列模型尽量避免随机 early stopping 验证集；如果使用随机划分，需要明确说明潜在数据泄漏风险。更推荐使用按时间顺序的验证集。
- 单只股票样本量较小，模型比较只能作为探索，不建议从一个标的得出泛化结论。
- 在 README 或 Notebook 结尾加入简洁结果表：模型、关键超参数、MSE、MAE、Pearson、是否超过基线。

## 建议下一步

把重复的评估代码抽成一个辅助函数，例如 `evaluate_predictions(y_true, y_pred, index=None)`，然后统一用于 Ridge、LightGBM 和 MLP。这样更方便横向比较，也能减少复制粘贴带来的错误。
