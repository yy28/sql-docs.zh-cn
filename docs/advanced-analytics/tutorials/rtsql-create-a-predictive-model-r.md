---
title: "创建预测模型 (SQL 快速入门中的 R) |Microsoft 文档"
ms.custom: 
ms.date: 07/26/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
dev_langs:
- R
- SQL
ms.assetid: 6eb78a80-5791-438f-9ca6-d142ab5d9bb1
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: On Demand
ms.openlocfilehash: 1b40295452da5b7da34a31e6825630da9c6c4861
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="create-a-predictive-model-r-in-sql-quickstart"></a>创建预测模型 (SQL 快速入门中的 R)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本步骤说明如何使用 R 训练模型，然后将该模型保存到 SQL Server 中的表。 该模型是一个简单的回归模型，可根据速度预测汽车的停止距离。 你将使用`cars`数据集包含使用 R，因为它小且易于理解。

## <a name="create-the-source-data"></a>创建源数据

首先，创建用于保存训练数据的表。

```sql
CREATE TABLE CarSpeed ([speed] int not null, [distance] int not null)
INSERT INTO CarSpeed
EXEC sp_execute_external_script
        @language = N'R'
        , @script = N'car_speed <- cars;'
        , @input_data_1 = N''
        , @output_data_1_name = N'car_speed'
```

+ 某些用户希望使用临时表，但请注意某些 R 客户端批处理之间的会话断开连接。

+ R 运行时包含许多或大或小的数据集。 若要获取随 R 一起安装的数据集列表，请在 R 命令提示符下键入 `library(help="datasets")`。

## <a name="create-a-regression-model"></a>创建回归模型

车速数据包含两个数字列：`dist` 和 `speed`。 某些速度有多个观察值。 将基于这些数据创建一个线性回归模型，用于描述车速与停车距离之间的某种关系。

线性模型的要求十分简单：

+ 定义一个公式用于描述因变量 `speed` 与自变量 `distance` 之间的关系

+ 提供用于训练模型的输入数据

> [!TIP]
> 如果你需要在线性模型使用刷新程序，我们建议本教程中，其中介绍了使用 rxLinMod 将模型拟合的过程：[拟合线性模型](https://docs.microsoft.com/r-server/r/how-to-revoscaler-linear-model)

若要实际生成模型，请在 R 代码中定义公式，然后将数据作为输入参数传递。

```sql
DROP PROCEDURE IF EXISTS generate_linear_model;
GO
CREATE PROCEDURE generate_linear_model
AS
BEGIN
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'lrmodel <- rxLinMod(formula = distance ~ speed, data = CarsData);
        trained_model <- data.frame(payload = as.raw(serialize(lrmodel, connection=NULL)));'
    , @input_data_1 = N'SELECT [speed], [distance] FROM CarSpeed'
    , @input_data_1_name = N'CarsData'
    , @output_data_1_name = N'trained_model'
    WITH RESULT SETS ((model varbinary(max)));
END;
GO
```

+ rxLinMod 的第一个参数是 *formula* 参数，定义与速度相关的距离。
+ 输入数据存储在 SQL 查询填充的变量 `CarsData` 中。 如果未将特定的名称分配到输入数据，默认变量名称将是 _InputDataSet_。

## <a name="create-a-table-for-storing-the-model"></a>创建用于存储模型的表

接下来，存储模型，以便可以重新训练，也可以将其用于预测。 创建模型的 R 包的输出通常是一个**二进制对象**。 因此，存储模型的表必须提供 **varbinary** 类型的列。

```sql
CREATE TABLE stopping_distance_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null);
```

## <a name="save-the-model"></a>保存模型

若要保存模型，请运行以下 Transact-SQL 语句调用存储过程，生成模型，然后将它保存到表中。

```sql
INSERT INTO stopping_distance_models (model)
EXEC generate_linear_model;
```

请注意，是否第二次运行此代码时，你会获得此错误：

```
Violation of PRIMARY KEY constraint...Cannot insert duplicate key in object dbo.stopping_distance_models
```

避免此错误的一种做法是更新每个新模型的名称。 例如，可将该名称更改为更具描述性的名称，并包含模型类型、创建日期，等等。

```sql
UPDATE stopping_distance_models
SET model_name = 'rxLinMod ' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
WHERE model_name = 'default model'
```

## <a name="output-additional-variables"></a>输出其他变量

通常，存储过程 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 的 R 输出仅限于单个数据框架。 （将来可能会去除此限制。）

但是，除数据框架以外，你还可以返回其他类型的输出，例如标量。

例如，假设你要训练某个模型，同时希望立即查看模型中的系数表。 可将系数表创建为主结果集，并在 SQL 变量中输出训练的模型。 你可以立即重新使用该模型通过调用该变量，或无法将模型保存到表中，如下所示。

```sql
DECLARE @model varbinary(max), @modelname varchar(30)
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
        speedmodel <- rxLinMod(distance ~ speed, CarsData)
        modelbin <- serialize(speedmodel, NULL)
        OutputDataSet <- data.frame(coefficients(speedmodel));'
    , @input_data_1 = N'SELECT [speed], [distance] FROM CarSpeed'
    , @input_data_1_name = N'CarsData'
    , @params = N'@modelbin varbinary(max) OUTPUT'
    , @modelbin = @model OUTPUT
    WITH RESULT SETS (([Coefficient] float not null));

-- Save the generated model
INSERT INTO [dbo].[stopping_distance_models] (model_name, model)
VALUES (' latest model', @model)
```

**结果**

![rslq_basictut_coefficients](media/rslq-basictut-coefficients.PNG)

### <a name="summary"></a>摘要

请记住使用 SQL 参数和 R 变量中的这些规则`sp_execute_external_script`:

+ 必须按名称的列出所有 SQL 参数映射到 R 脚本 _@params_ 自变量。
+ 若要输出其中一个参数，请在 _@params_ 列表中添加 OUTPUT 关键字。
+ 列出映射的参数后，请紧接在 _@params_ 列表的后面，逐行提供 SQL 参数到 R 变量的映射。

## <a name="next-lesson"></a>下一课

现已创建一个模型。最后一个步骤将说明如何通过该模型生成预测并绘制结果。

[通过模型预测和绘图](../tutorials/rtsql-predict-and-plot-from-model.md)


