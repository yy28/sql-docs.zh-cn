---
title: 创建和导出 Spark 机器学习模型与 MLeap
titleSuffix: SQL Server big data clusters
description: 使用 PySpark 训练和 SQL Server 大数据群集 （预览版） 上创建 Spark 机器学习模型。 导出包含 MLeap，然后在 SQL Server 中评分与 Java 配合使用的模型。
author: lgongmsft
ms.author: lgong
ms.reviewer: mikeray
ms.date: 06/26/2019
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: aa4c31eca725e8e662937259f078cf00a3441915
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/10/2019
ms.locfileid: "67727373"
---
# <a name="create-export-and-score-spark-machine-learning-models-on-sql-server-big-data-clusters"></a>创建、 导出和 SQL Server 大数据群集上评分 Spark 机器学习模型

下面的示例演示如何使用构建模型[Spark 机器学习](https://spark.apache.org/docs/latest/ml-guide.html)，导出到模型[MLeap](http://mleap-docs.combust.ml/)，和在 SQL Server 中评分模型及其[Java 语言扩展](../language-extensions/language-extensions-overview.md)。 这是在 SQL Server 2019 大数据群集上下文。

下图说明了在此示例中所执行的工作：

![使用 spark 的训练分数导出](./media/spark-create-machine-learning-model/train-score-export-with-spark.png)

## <a name="prerequisites"></a>先决条件

本示例的所有文件都将位于[ https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml ](https://github.com/microsoft/sql-server-samples/tree/master/samples/features/sql-big-data-cluster/spark/sparkml)。

若要运行示例，还必须具备以下先决条件：

- 一个[SQL Server 大数据群集](deploy-get-started.md)

- [大数据工具](deploy-big-data-tools.md)
   - **kubectl**
   - **curl**
   - **Azure Data Studio**

## <a name="model-training-with-spark-ml"></a>使用 Spark ML 模型训练

对于此示例中，人口普查数据 (**AdultCensusIncome.csv**) 用于生成 Spark ML 管道模型。

1. 使用[mleap_sql_test/setup.sh](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/setup.sh)文件从 internet 下载数据集并将其放在 HDFS 上 SQL Server 大数据群集中。 这使它能够访问由 Spark。

1. 然后下载示例笔记本[train_score_export_ml_models_with_spark.ipynb](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb)。 从 PowerShell 或 bash 命令行运行以下命令以下载笔记本：

   ```PowerShell
   curl -o mssql_spark_connector.ipynb "https://raw.githubusercontent.com/microsoft/sql-server-samples/master/samples/features/sql-big-data-cluster/spark/sparkml/train_score_export_ml_models_with_spark.ipynb"
   ```

   此笔记本包含具有所需的命令示例的此部分的单元格。

1. 在 Azure 数据工作室中打开笔记本并运行每个代码块。 有关使用笔记本的详细信息，请参阅[如何在 SQL Server 2019 预览版中使用笔记本](notebooks-guidance.md)。

第一次读取到 Spark 数据并将其拆分为定型集和测试数据集。 然后代码训练管道模型的定型数据。 最后，它将模型导出到一个 MLeap 捆绑包。

> [!TIP]
> 您还可以查看或运行中的 notebook 之外的这些步骤与关联的 Python 代码[mleap_sql_test/mleap_pyspark.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_pyspark.py)文件。

## <a name="model-scoring-with-sql-server"></a>模型评分与 SQL Server

现在，Spark ML 管道模型处于常见序列化[MLeap 捆绑](http://mleap-docs.combust.ml/core-concepts/mleap-bundles.html)格式，可以评分不需要 Spark 在 Java 中的模型。 

此示例使用[Java 语言扩展](../language-extensions/language-extensions-overview.md)SQL Server 中。 若要在 SQL Server 中评分模型，首先需要构建可以加载到 Java 模型并为其评分的 Java 应用程序。 可以为此 Java 应用程序中找到的示例代码[mssql mleap 应用文件夹](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mssql-mleap-app)。

生成示例之后, 可以使用 TRANSACT-SQL 来调用的 Java 应用程序并与数据库表模型评分。 这可在三个[mleap_sql_test/mleap_sql_tests.py](https://github.com/microsoft/sql-server-samples/blob/master/samples/features/sql-big-data-cluster/spark/sparklm/mleap_sql_test/mleap_sql_tests.py)源文件。

## <a name="next-steps"></a>后续步骤

有关大数据群集的详细信息，请参阅[如何部署 SQL Server 大数据群集在 Kubernetes 上](deployment-guidance.md)
