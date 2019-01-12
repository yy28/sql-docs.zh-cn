---
title: 导出具有 MLeap 的 Spark 机器学习模型
titleSuffix: SQL Server 2019 big data clusters
description: 了解如何导出 Spark 机器学习具有 MLeap 的模型。
author: lgongmsft
ms.author: shivprashant
ms.reviewer: jroth
manager: craigg
ms.date: 12/06/2018
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.custom: seodec18
ms.openlocfilehash: ee858f66c99ff7b85e2e6c456ad509ec7deb0a6e
ms.sourcegitcommit: 202ef5b24ed6765c7aaada9c2f4443372064bd60
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2019
ms.locfileid: "54242128"
---
# <a name="export-spark-machine-learning-models-with-mleap"></a>导出 Spark 机器学习模型与 MLeap

典型的机器学习方案涉及在 Spark 中的模型训练和评分外部 Spark。 导出可移植格式中的模型，以便它可以使用外部 Spark。 [MLeap](https://github.com/combust/mleap)是一个此类模型交换格式。 它允许 Spark 机器学习管道和模型能够被导出为可移植格式并在任何基于 JVM 的系统中使用`Mleap`运行时。

本指南演示如何将导出使用 Mleap spark 模型。 步骤总结如下，并详细的下列部分中的代码。

1. 首先创建一个 Spark 模型。 为此，请使用**定型集和创建机器学习模型与 Spark[此处。](train-and-create-machinelearning-models-with-spark.md)**
2. 下一步，我们将**导入 training\test 数据和模型**
3. **导出将模型作为`Mleap`捆绑**。 此导出的捆绑包现在可用于外部 spark 评分。
4. 若要验证，我们将导入`Mleap`捆绑后再次并使用它来在 Spark 中评分。

## <a name="step-1---start-by-creating-a-spark-model"></a>步骤 1-通过创建 Spark 模型开始
运行[定型集和创建机器学习模型与 Spark](train-and-create-machinelearning-models-with-spark.md)创建训练/测试集和模型，并将保存到 HDFS 存储。 该模型应导出作为`AdultCensus.mml`下`spark_ml`目录。

## <a name="step-2---import-the-trainingtest-data-and-the-model"></a>步骤 2-导入 training\test 数据和模型

步骤 1 创建`AdultCensus.mml`，这是 spark 模型。 

在此步骤中，导入 spark 模型。

```python
import mleap.pyspark
from mleap.pyspark.spark_support import SimpleSparkSerializer
from pyspark.ml import PipelineModel

model_name = "AdultCensus.mml"
model_fs = "/spark_ml/" + model_name

print("load pyspark model from hbfs")
model = PipelineModel.load(model_fs)
print("Model is " , model)
print("Model stages", model.stages)
```

## <a name="step-3---export-the-model-as-mleap-bundle"></a>步骤 3-导出该模型作为`Mleap`捆绑包

将 Spark 模型导出为可移植`Mleap`模型并将其保留在本地存储中。 发布此步骤中，模型位于可移植`Mleap`格式化并可以使用外部 Spark。

```python
import os

#Get the train and test datasets

# Write the train and test data sets to intermediate storage

train_data_path = "/spark_ml/AdultCensusIncomeTrain"
test_data_path = "/spark_ml/AdultCensusIncomeTest"

train = spark.read.orc(train_data_path)
test = spark.read.orc(test_data_path)

print("train: ({}, {})".format(train.count(), len(train.columns)))
train.printSchema()

print("test: ({}, {})".format(test.count(), len(test.columns)))
test.printSchema()

# serialize the model to a zip file in JSON format
model_name_export = "adult_census_pipeline.zip"
model_name_path = os.getcwd()
model_file = os.path.join(model_name_path, model_name_export)

# serialize the model to a zip file in JSON format
model_name_export = "adult_census_pipeline.zip"
model_name_path = os.getcwd()
model_file = os.path.join(model_name_path, model_name_export)

# remove an old model file, if needed.
try:
    os.remove(model_file)
except OSError:
    pass

model_file_path = "jar:file:{}".format(model_file)
model.serializeToBundle(model_file_path, model.transform(train))

```

保留`Mleap`从本地到 hdfs 的捆绑包

```python
print("persist the mleap bundle from local to hdfs")
from subprocess import Popen, PIPE
proc = Popen(["hadoop", "fs", "-put", "-f", model_file, os.path.join("/spark_ml", model_name_export)], stdout=PIPE, stderr=PIPE)
s_output, s_err = proc.communicate()
if(s_err):
    print("Error when storing to HDFS")
```

## <a name="step-3---validate-by-importing-the-mleap-bundle-and-scoring-in-spark"></a>步骤 3-通过导入来验证`Mleap`捆绑包并在 Spark 中的评分
在步骤 2 中，我们已将导出该模型可移植到`Mleap`外部 Spark 可以使用的格式。 在此步骤中，我们导入`Mleap`在 Spark 中序列化并使用它对分数的 Spark 中对测试集。
   
```python
model_deserialized = PipelineModel.deserializeFromBundle(model_file_path)
print("The deserialized model is ", model_deserialized)
print("The deserialized model stages are", model_deserialized.stages)

from pyspark.ml.evaluation import BinaryClassificationEvaluator

# make prediction
pred = model_deserialized.transform(test)


# evaluate. note only 2 metrics are supported out of the box by Spark ML.
bce = BinaryClassificationEvaluator(rawPredictionCol='rawPrediction')
au_roc = bce.setMetricName('areaUnderROC').evaluate(pred)
au_prc = bce.setMetricName('areaUnderPR').evaluate(pred)

print("Results of using the model score test set")
print("Area under ROC: {}".format(au_roc))
print("Area Under PR: {}".format(au_prc))
```

## <a name="references"></a>References

* [开始使用 PySpark 笔记本](notebooks-guidance.md)
* [定型集和使用 Spark 创建机器学习模型](train-and-create-machinelearning-models-with-spark.md)
