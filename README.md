# test_run

这是一个使用单只股票数据测试机器学习模型的探索项目。

## 内容

- `single_stock.ipynb`：数据检查、Alpha158 特征生成、按时间划分训练集/验证集/测试集、Ridge、LightGBM、MLP 以及模型可视化。
- `tech_stock.csv`：Notebook 流程中使用的单只股票 OHLCV 示例数据。

## 环境准备

```bash
python -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
cp .env.example .env
```

运行 Notebook 前，需要在 `.env` 中填写数据库和 Qlib 路径：

```text
MYSQL_HOST=
MYSQL_USER=
MYSQL_PASSWORD=
MYSQL_DATABASE=intern
QLIB_PROVIDER_URI=
```

## 可复现性说明

- 数据库账号、密码和本地 token 应放在 `.env` 中，不要提交到 git。
- 生成的 Qlib 二进制数据建议放在 git 之外，或放到已忽略的 `qlib_data/` 目录。
- 训练集、验证集、测试集应按时间顺序划分。
