---
title: 使用 Spark 的训练/创建机器学习模型
titleSuffix: SQL Server 2019 big data clusters
description: 使用 PySpark 训练和 SQL Server 大数据群集 （预览版） 上创建 Spark 机器学习模型。
author: lgongmsft
ms.author: shivprashant
ms.manager: craigg
ms.reviewer: jroth
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: 1ef8f66d220561407c0bcafedde8a402f871924a
ms.sourcegitcommit: 8bc5d85bd157f9cfd52245d23062d150b76066ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2019
ms.locfileid: "57578107"
---
# <a name="train-and-create-machine-learning-models-with-spark"></a>训练和创建 Spark 的机器学习模型

SQL Server 大数据群集中的 Spark，AI 和机器学习。 该示例演示如何培训机器学习模型在 Spark (PySpark) 使用的数据中使用 Python 存储在 HDFS 中。 

该示例是一次和代码片段，可从 Azure 数据 Studio Notebook 并运行每个单元格的一个步骤的分步指南。 如何将 Spark 连接从笔记本中的详细信息，请参阅[此处](notebooks-guidance.md)

在下面的示例：

1. 使用启动**了解数据和所需的预测**
2. **将数据上载到 HDFS 和准备数据**用于创建模型
3. **选择要使用的功能**
4. **将数据拆分为训练和测试集**
5. 将组合在一起**ml 管道并生成一个模型**
6. 使用创建的模型为**进行预测**
7. 最后一步**持久保存创建的模型以更高版本使用**。

E2E 机器学习涉及几个额外的步骤，例如、 数据浏览、 功能选择和主体组件分析、 模型选择。 许多这些步骤将为简洁起见此处忽略。

## <a name="step-1---understanding-the-data-and-prediction-desired"></a>步骤 1-了解数据和所需的预测

此示例使用从成人人口普查数据[此处]( https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv )。 在`AdultCensusIncome.csv`、 每个行表示收入范围和其他特征等 age，每周小时数教育、 职业等的给定成人。 生成一个模型，如果可预测收入范围。 该模型将获取年龄和作为功能每周小时数，并预测收入会 > 50 K 或 < 50 k。 

## <a name="step-2---upload-the-data-to-hdfs-and-basic-explorations-on-data"></a>步骤 2-将数据上载到 HDFS 和基本数据探索
从 Azure Data Studio 连接到 HDFS/Spark 网关，并创建一个名为目录`spark_ml`下 HDFS。 下载[AdultCensusIncome.csv]( https://amldockerdatasets.azureedge.net/AdultCensusIncome.csv )到本地计算机和上的传到 HDFS。 上传`AdultCensusIncome.csv`你创建的文件夹。


现在，编写一些代码。 可以复制以下代码，并将它粘贴到 notebook Azure Data Studio 中的各个单元格。 

下面的代码读取到 Spark 数据框架的 CSV 文件。 进一步的它的行和列进行计数，并显示加载的数据。

```python
datafile = "/spark_ml/AdultCensusIncome.csv"

#Read the data to a spark data frame.
data_all = spark.read.format('csv').options(header='true', inferSchema='true', ignoreLeadingWhiteSpace='true', ignoreTrailingWhiteSpace='true').load(datafile)
print("Number of rows: {},  Number of coulumns : {}".format(data_all.count(), len(data_all.columns)))

#Replace "-" with "_" in column names
columns_new = [col.replace("-", "_") for col in data_all.columns]
data_all = data_all.toDF(*columns_new)

#Print Schema and show top 5 row
data_all.printSchema() 
data_all.show(5)
```

## <a name="step-3---select-features-to-use"></a>步骤 3-选择要使用的功能

在此步骤中，使用以下两个术语
1. `Label`    -是指要预测的值。 这表示为数据中的列。  
2. `Features` -是指要预测的数据中的特征。 也可以简称为一些时间 `predictors` 

在此示例中`Label`，是**收入**列。 为简单起见，选择**年龄**并**hours_per_week**作为`Features`。 在现实中选择功能通过应用一些相关的技术，这样可以了解什么最适合描述 predicting 标签特征。

```python
# Choose feature columns and the label column.
label = "income"
xvars = ["age", "hours_per_week"] #all numeric

print("label = {}".format(label))
print("features = {}".format(xvars))

select_cols = xvars
select_cols.append(label)
data = data_all.select(select_cols)

```

## <a name="step-4---split-as-training-and-test-set"></a>步骤 4-拆分为训练和测试集

使用 75%的行来定型模型和 25%，以便评估模型的其余部分。 此外，持久保存定型和测试到 HDFS 存储的数据集。 步骤不是必需的但所示，若要演示如何保存和加载具有 ORC 格式。 其他格式，例如， `Parquet` ，也可以使用。

发布此步骤中应会看到两个目录创建具有名称 AdultCensusIncomeTrain 和 AdultCensusIncomeTest

```python

# Split data into train and test.
train, test = data.randomSplit([0.75, 0.25], seed=123)

print("train ({}, {})".format(train.count(), len(train.columns)))
print("test ({}, {})".format(test.count(), len(test.columns)))

train_data_path = "/spark_ml/AdultCensusIncomeTrain"
test_data_path = "/spark_ml/AdultCensusIncomeTest"

train.write.mode('overwrite').orc(train_data_path)
test.write.mode('overwrite').orc(test_data_path)
print("train and test datasets saved to {} and {}".format(train_data_path, test_data_path))

```

## <a name="step-5---put-together-a-pipeline-and-build-a-model"></a>步骤 5-将汇总到一个管道并生成一个模型
[Spark ML 管道](https://spark.apache.org/docs/2.3.1/ml-pipeline.html)允许工作流的形式进行排序的所有步骤，使其更轻松地使用各种算法和其参数进行试验。 下面的代码首先构造阶段，然后将这些阶段一起放在机器学习管道中。  LogisticRegression 用于创建模型。

```python
from pyspark.ml import Pipeline, PipelineModel
from pyspark.ml.feature import OneHotEncoder, StringIndexer, VectorAssembler
from pyspark.ml.classification import LogisticRegression

reg = 0.1
print("Using LogisticRegression model with Regularization Rate of {}.".format(reg))

# create a new Logistic Regression model.
lr = LogisticRegression(regParam=reg)

dtypes = dict(train.dtypes)
dtypes.pop(label)

si_xvars = []
ohe_xvars = []
featureCols = []
for idx,key in enumerate(dtypes):
    if dtypes[key] == "string":
        featureCol = "-".join([key, "encoded"])
        featureCols.append(featureCol)
        
        tmpCol = "-".join([key, "tmp"])
        si_xvars.append(StringIndexer(inputCol=key, outputCol=tmpCol, handleInvalid="skip")) #, handleInvalid="keep"
        ohe_xvars.append(OneHotEncoder(inputCol=tmpCol, outputCol=featureCol))
    else:
        featureCols.append(key)

# string-index the label column into a column named "label"
si_label = StringIndexer(inputCol=label, outputCol='label')

# assemble the encoded feature columns in to a column named "features"
assembler = VectorAssembler(inputCols=featureCols, outputCol="features")

```

现在，将汇总到管道。 

```python
# put together the pipeline
stages = []
stages.extend(si_xvars)
stages.extend(ohe_xvars)
stages.append(si_label)
stages.append(assembler)
stages.append(lr)
pipe = Pipeline(stages=stages)
print("Pipeline Created")

```

现在，创建管道，则可使用它来训练该模型。

```python
# train the model
model = pipe.fit(train)
print("Model Trained")
print("Model is ", model)
print("Model Stages", model.stages)

```

## <a name="step-6---predict-using-the-model-and-evaluate-the-model-accuracy"></a>步骤 6-使用该模型进行预测并评估模型准确性
下面的代码使用测试数据集来预测使用在前面步骤中创建的模型的结果。 度量值与模型的准确性`areaUnderROC`和`areaUnderPR`指标。

```python
from pyspark.ml.evaluation import BinaryClassificationEvaluator
# make prediction
pred = model.transform(test)

# evaluate. note only 2 metrics are supported out of the box by Spark ML.
bce = BinaryClassificationEvaluator(rawPredictionCol='rawPrediction')
au_roc = bce.setMetricName('areaUnderROC').evaluate(pred)
au_prc = bce.setMetricName('areaUnderPR').evaluate(pred)

print("Area under ROC: {}".format(au_roc))
print("Area Under PR: {}".format(au_prc))
```


## <a name="step-7---persist-the-models-to-hdfs"></a>步骤 7-持久保存到 HDFS 的模型
最后，保存在 HDFS 中的模型以供将来使用。 发布此步骤中创建的模型获取另存为 /spark_ml/AdultCensus.mml

```python
##NOTE: by default the model is saved to and loaded from path

model_name = "AdultCensus.mml"
model_fs = "/spark_ml/" + model_name

model.write().overwrite().save(model_fs)
print("saved model to {}".format(model_fs))

# load the model file (from dbfs)
model2 = PipelineModel.load(model_fs)
assert str(model2) == str(model)
print("loaded model from {}".format(model_fs))
```

## <a name="next-steps"></a>后续步骤

有关如何开始使用 PySpark 笔记本的详细信息，请参阅[如何使用笔记本](notebooks-guidance.md)。