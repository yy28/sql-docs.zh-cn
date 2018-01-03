---
title: "使用 Azure SQL 数据库中的 R |Microsoft 文档"
ms.custom: 
ms.date: 12/08/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: r
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 0a90c438-d78b-47be-ac05-479de64378b2
caps.latest.revision: "1"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.openlocfilehash: 8960f8a8c5dadaa0c53cd4fcb1ab786ce6e720a7
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/02/2018
---
# <a name="using-r-in-azure-sql-database"></a>在 Azure SQL Database 中使用 R

自 2017 年 10 月，就是在 SQL Server 开发团队宣布计划来支持的 R 代码数据库中使用类似于 SQL Server 2016 中的 R Services 的存储的过程的执行。 

若要保持最新公开发布的版本计划和即将到来的事件，请参阅[SQL Server 博客](https://blogs.technet.microsoft.com/dataplatforminsider/)或[Microsoft R Server 博客](https://blogs.msdn.microsoft.com/rserver/)。

> [!IMPORTANT]
> 目前，R 支持预览仅在中央美国西部的 Azure SQL 数据库提供版，功能将受到限制 R 的功能比较和 Python 代码在 SQL Server 2016 或自 2017 年中的执行。

## <a name="whats-included"></a>包含的内容

可以在以下数据库服务层和性能级别上使用的数据库中 R 功能：
 
- 高级服务层 – P1、 P2、 P4、 P6、 P11、 P15
- 高级 RS 服务层级 – PRS1，PRS2，PRS4，PRS6
- 高级弹性池 – 125 弹性 Dtu 或更高版本
- 高级 RS 弹性池 – 125 弹性 Dtu 或更高版本

预览版本包括这些包：

+   Microsoft R Open 使用 R 版本 3.3.3
+   基本 R 包和函数一起预装
+   Microsoft R Server 9.2，包括 RevoScaleR 包

在当前的预览版本中，你可以执行以下任务：

+ 使用适合在内存中的任何数据模型的训练
+   使用适合在内存中的任何数据模型的评分
+   执行 R 脚本的普通并行度 (使用@parallel中 sp_execute_external_script 参数)
+   流式处理执行 R 脚本的执行 (使用@r_RowsPerRead中 sp_execute_external_script 参数)
+   一次执行一个 R 脚本


在 Azure SQL 数据库上的 R 的预览版本中不支持以下任务：

+ 无法启用对特定数据库执行的 R 脚本。
+ Dmv 提供监视 CPU 和内存使用情况的 R 脚本将不可用。
+ 可以不安装任何第三方程序包。 不支持创建外部库语句。

## <a name="example"></a>示例

Azure SQL DB 中 R 运行的所有命令从 T-SQL，使用存储的过程[sp_execute_external_script](https://docs.microsoft.com/sql/relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql)。 

下面的示例演示如何以试用预览功能，使用 iris 数据集包含基。

### <a name="step-1-create-the-data-tables"></a>步骤 1. 创建数据表

首先创建两个表： 一个用于存储从 R，提取的源数据，一个用于存储经过训练的模型。

```sql
DROP TABLE IF EXISTS iris_data, iris_models;
GO
CREATE TABLE iris_data (
        id INT NOT NULL IDENTITY PRIMARY KEY
        , "Sepal.Length" FLOAT NOT NULL, "Sepal.Width" FLOAT NOT NULL
        , "Petal.Length" FLOAT NOT NULL, "Petal.Width" FLOAT NOT NULL
        , "Species" VARCHAR(100) NULL
);
CREATE TABLE iris_models (
    model_name VARCHAR(30) NOT NULL PRIMARY KEY,
    model VARBINARY(max) NOT NULL,
    native_model VARBINARY(MAX) NOT NULL
);
GO
```

### <a name="step-2-populate-table-with-data-from-the-iris-dataset"></a>步骤 2. 数据来自 iris 数据集表中填充

在创建的表后，运行以下代码以将定型数据插入表。 存储的过程 sp_execute_external_script 调用 R，并返回 iris 数据集作为数据框架，使用 INSERT INTO 语句中指定的架构。

```sql
INSERT INTO iris_data
("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
EXEC sp_execute_external_script @language = N'R'
  , @script = N'iris_data <- iris;'
  , @input_data_1 = N''
  , @output_data_1_name = N'iris_data';
GO
```

### <a name="step-3-create-the-stored-procedure-that-generates-the-model"></a>步骤 3. 创建生成模型的存储的过程

以下存储的过程执行实际创建并定型模型，可以采用两种二进制格式保存该的操作。

```sql
CREATE PROCEDURE generate_iris_model
    @trained_model VARBINARY(MAX) OUTPUT, 
    @native_trained_model VARBINARY(MAX) OUTPUT
AS
BEGIN
  EXEC sp_execute_external_script @language = N'R'
  , @script = N'
    iris_model <- rxDTree(Species ~ Sepal.Length + Sepal.Width + Petal.Length + Petal.Width, data = iris_rx_data);
    trained_model <- as.raw(serialize(iris_model, connection=NULL));
    native_trained_model <- rxSerializeModel(iris_model, realtimeScoringOnly = TRUE)
    '
  , @input_data_1 = N'SELECT "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" FROM iris_data'
  , @input_data_1_name = N'iris_rx_data'
  , @params = N'@trained_model VARBINARY(MAX) OUTPUT, @native_trained_model VARBINARY(MAX) OUTPUT
    , @trained_model = @trained_model OUTPUT
    , @native_trained_model = @native_trained_model OUTPUT;
End
```

+ **输出**上的输入参数的关键字表示应传递和用于输出以及值。
+ 以开头的行`iris_model`定义决策树模型来预测指定基于花属性。
+ 调用`serialize`中的二进制格式的模型适用于 SQL Server 中存储的节省。 
+ 或者，对于基于 RevoScaleR 算法的模型，你可以使用[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)函数，将模型保存在新的本机二进制格式。 为的评分与 SQL Server 中的预测函数加载模型保存在此格式。

### <a name="step-4-train-and-save-the-model"></a>步骤 4. 训练和保存模型

创建存储的过程后，调用它可处理输入的数据并创建模型。 下面的代码还将模型保存到表**iris_models**，以便你可以使用它更高版本来预测的花指定。

```sql
DECLARE @model VARBINARY(MAX), @native_modelVARBINARY(MAX);
EXEC generate_iris_model @model OUTPUT, @native_model OUTPUT;
DELETE FROM iris_models WHERE model_name = 'iris.dtree';
INSERT INTO iris_models (model_name, model, native_model) VALUES('iris.dtree', @model, @native_model);
SELECT model_name, datalength(model)/1024. AS model_size_kb, datalength(native_model)/1024. AS native_model_size_kb FROM iris_models;
GO
```

### <a name="step-5-create-a-stored-procedure-for-scoring"></a>步骤 5. 创建存储的过程以获得评分

接下来，创建存储的过程以获得评分。 此存储的过程从表中，加载指定的模型，并创建根据输入数据评分。

```sql
CREATE PROCEDURE predict_iris_species (@model varchar(100))
AS
BEGIN
  DECLARE @rx_model VARBINARY(MAX) = (SELECT model FROM iris_models WHERE model_name = @model);
  EXEC sp_execute_external_script @language = N'R'
  , @script = N'
    irismodel<-unserialize(rx_model);
    OutputDataSet <-rxPredict(irismodel, iris_rx_data, extraVarsToWrite = c("Species", "id"));
      '
  , @input_data_1 = N'SELECT "id", "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" FROM iris_data'
  , @input_data_1_name = N'iris_rx_data'
  , @params = N'@rx_model varbinary(max)'
  , @rx_model = @rx_model
  WITH RESULT SETS ( ("setosa_Pred" FLOAT, "versicolor_Pred" FLOAT, "virginica_Pred" FLOAT, "Species.Actual" VARCHAR(100), "id" INT));
END;
GO
```

此存储过程使用[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)函数，但你可以还使用本机的预测函数在 T-SQL 中所示[此处](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2017/09/25/announcing-general-availability-of-native-scoring-using-predict-function-in-azure-sql-database/)。 预测函数的用法要求你使用[ **rx**模型](https://docs.microsoft.com/machine-learning-server/r/concept-what-is-revoscaler)并保存模型使用[rxSerializeModel](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxserializemodel)。

### <a name="step-6-use-the-stored-procedure-to-generate-predictions"></a>步骤 6. 使用存储的过程来生成预测

若要从模型生成分数，请运行存储的过程。 你可以将值插入表，或返回到调用应用程序的预测。

```sql
EXEC predict_iris_species 'iris.dtree';
GO
```

## <a name="related-resources"></a>相关资源

Azure 应用商店还提供了包括 SQL Server 自 2017 年的多个虚拟机：

+ [设置用于在 Azure 上的机器学习的虚拟机](provision-the-r-server-only-sql-server-2016-enterprise-vm-on-azure.md)

同时查看这些 Vm，但这与各种受欢迎的机器学习工具都被预配置：

+ [数据科学虚拟机](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/overview)
+ [深入学习虚拟机](https://docs.microsoft.com/azure/machine-learning/data-science-virtual-machine/deep-learning-dsvm-overview)

