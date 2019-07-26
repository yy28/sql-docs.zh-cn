---
title: 使用 R 创建预测模型的快速入门
description: 在本快速入门教程中, 了解如何使用 SQL Server 数据来绘制预测, 以在 R 中构建模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 7de37b16c04cf2f972e36c11ba5dfb53721e6094
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469435"
---
# <a name="quickstart-create-a-predictive-model-using-r-in-sql-server"></a>快速入门：在 SQL Server 中使用 R 创建预测模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入门中, 你将了解如何使用 R 为模型定型, 然后将该模型保存到 SQL Server 中的表。 该模型是一个简单的通用线性模型 (GLM), 该模型预测车辆经过手动传输的概率。 你将使用 R `mtcars`附带的数据集。

## <a name="prerequisites"></a>先决条件

以前的快速入门,[验证 SQL Server 中是否存在 r](quickstart-r-verify.md), 提供了设置本快速入门所需的 R 环境的信息和链接。

## <a name="create-the-source-data"></a>创建源数据

首先，创建用于保存训练数据的表。

```sql
CREATE TABLE dbo.MTCars(
    mpg decimal(10, 1) NOT NULL,
    cyl int NOT NULL,
    disp decimal(10, 1) NOT NULL,
    hp int NOT NULL,
    drat decimal(10, 2) NOT NULL,
    wt decimal(10, 3) NOT NULL,
    qsec decimal(10, 2) NOT NULL,
    vs int NOT NULL,
    am int NOT NULL,
    gear int NOT NULL,
    carb int NOT NULL
);
```

接下来, 从数据集中`mtcars`的生成中插入数据。

```SQL
INSERT INTO dbo.MTCars
EXEC sp_execute_external_script
        @language = N'R'
        , @script = N'MTCars <- mtcars;'
        , @input_data_1 = N''
        , @output_data_1_name = N'MTCars';
```

+ 有些人喜欢使用临时表, 但请注意, 某些 R 客户端在批处理之间断开会话连接。

+ R 运行时包含许多或大或小的数据集。 若要获取随 R 一起安装的数据集列表，请在 R 命令提示符下键入 `library(help="datasets")`。

## <a name="create-a-model"></a>创建模型

Car 速度数据包含两列: 数值、动力 (`hp`) 和权重 (`wt`)。 在此数据中, 你将创建一个通用线性模型 (GLM), 该模型会估算车辆已调整为手动传输的概率。

若要生成模型, 请在 R 代码中定义公式, 并将数据作为输入参数传递。

```sql
DROP PROCEDURE IF EXISTS generate_GLM;
GO
CREATE PROCEDURE generate_GLM
AS
BEGIN
    EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'carsModel <- glm(formula = am ~ hp + wt, data = MTCarsData, family = binomial);
        trained_model <- data.frame(payload = as.raw(serialize(carsModel, connection=NULL)));'
    , @input_data_1 = N'SELECT hp, wt, am FROM MTCars'
    , @input_data_1_name = N'MTCarsData'
    , @output_data_1_name = N'trained_model'
    WITH RESULT SETS ((model VARBINARY(max)));
END;
GO
```

+ 的第一个参数`glm`是*公式*参数, 该参数`am` `hp + wt`定义为依赖于。
+ 输入数据存储在 SQL 查询填充的变量 `MTCarsData` 中。 如果未将特定的名称分配到输入数据，默认变量名称将是 _InputDataSet_。

## <a name="create-a-table-for-the-model"></a>为模型创建表

接下来, 存储模型, 以便可以重新训练或将其用于预测。 创建模型的 R 包的输出通常是一个**二进制对象**。 因此, 存储模型的表必须提供**varbinary (max)** 类型的列。

```sql
CREATE TABLE GLM_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
```

## <a name="save-the-model"></a>保存模型

若要保存模型，请运行以下 Transact-SQL 语句调用存储过程，生成模型，然后将它保存到表中。

```sql
INSERT INTO GLM_models(model)
EXEC generate_GLM;
```

请注意, 如果第二次运行此代码, 将收到此错误:

```sql
Violation of PRIMARY KEY constraint...Cannot insert duplicate key in object dbo.stopping_distance_models
```

避免此错误的一种做法是更新每个新模型的名称。 例如，可将该名称更改为更具描述性的名称，并包含模型类型、创建日期，等等。

```sql
UPDATE GLM_models
SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
WHERE model_name = 'default model'
```

## <a name="next-steps"></a>后续步骤

现在, 你已有了一个模型, 在最后的快速入门中, 你将了解如何根据其生成预测并绘制结果。

> [!div class="nextstepaction"]
> [起步从模型预测和绘图](quickstart-r-predict-from-model.md)