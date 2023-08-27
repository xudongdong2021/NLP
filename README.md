### 商品命名实体识别（基于BERT预训练微调）

背景/需求

```
企业中产品的名称复杂，在对客户进行AI回访时，需要精简产品名称以提高效率和客户服务体验。因此，思路是提取复杂产品名称中的实体，将其转化为品牌+产品种类。例如，转化为“海尔”+“冰箱”。此项目就是实现该目的。结论是，基本能够满足实际要求，但仍需一定的人工审查。
```

目录结构及说明

```python
main
--data_process  # 数据处理模块
	--data_proc.ipynb  # 数据处理
	--data_verification.ipynb  # 数据校验
	--labels_note.txt  # 标签说明
--model  # 预训练微调模型参数存放（未上传）
	--config.json
	--pytorch_model.bin
	--vocab.txt
--ProductNER.ipynb  # 模型训练(main)
--Pred.ipynb  # 模型预测
--pred.csv  # 预测结果
```

requirements

```python
pandas == 2.0.3
torch == 1.12.1
transformers == 4.32.0
scikit-learn == 1.3.0
```

思路

```
1、对原始数据进行处理，尽可能去除杂质
--eg:"●GR-RF541WE-PG1A8(墨茶棕)东芝冰箱515升电冰箱" -> "东 芝 冰 箱 电 冰 箱"
2、构建数据集
--标签为BIO模式，详情见labels_note.txt文件
3、利用BERT预训练模型进行微调
--训练集准确率为0.9896，验证集为0.9729
4、读取源数据，并利用模型生成相应的产品名称
--见Pred.ipynb（预测过程）和pred.csv（预测结果）
```

TO DO

```
1、扩展：构建家居产品数据集
2、对比spacy命名实体识别
3、如何更不费力地构建数据集进行训练？
4、是否有其他方法（比如完全用正则进行处理）？
```

