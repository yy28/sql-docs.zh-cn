---
title: 创建使用 R 的 SQL Server 机器学习的预测模型的快速入门
description: 在本快速入门，了解如何生成在 R 中使用 SQL Server 数据绘制的预测模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 278eba1189b376b57f2dec7249a378832c18095c
ms.sourcegitcommit: baca29731a1be4f8fa47567888278394966e2af7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/04/2019
ms.locfileid: "54046753"
---
# <a name="quickstart-create-a-predictive-model-using-r-in-sql-server"></a>快速入门：创建在 SQL Server 中使用 R 预测模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在此快速入门中，将了解如何使用 R、 对模型定型，然后将该模型保存到 SQL Server 中的表。 该模型是一个简单通用线性模型 (GLM) 的预测概率某辆车已裝手动传输。 将使用`mtcars`包含的数据集

## <a name="prerequisites"></a>先决条件

上一个快速入门中， [SQL Server 中存在验证 R](quickstart-r-verify.md)、 提供的信息和链接设置为本快速入门所需的 R 环境。

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

接下来，将数据插入从数据集中生成`mtcars`。

```SQL
INSERT INTO dbo.MTCars
EXEC sp_execute_external_script
        @language = N'R'
        , @script = N'MTCars <- mtcars;'
        , @input_data_1 = N''
        , @output_data_1_name = N'MTCars';
```

+ 一些人喜欢使用临时表，但请注意某些 R 客户端断开批之间的会话。

+ R 运行时包含许多或大或小的数据集。 若要获取随 R 一起安装的数据集列表，请在 R 命令提示符下键入 `library(help="datasets")`。

## <a name="create-a-model"></a>创建模型

车速数据包含两个列，这两个数值、 马力 (`hp`) 和权重 (`wt`)。 通过此数据，您将创建估计某辆车已裝手动传输的概率的通用线性模型 (GLM)。

若要生成模型，R 代码内定义的公式，并将数据传递作为输入参数。

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

+ 第一个参数`glm`是*公式*参数，它定义`am`依赖于`hp + wt`。
+ 输入数据存储在 SQL 查询填充的变量 `MTCarsData` 中。 如果未将特定的名称分配到输入数据，默认变量名称将是 _InputDataSet_。

## <a name="create-a-table-for-the-model"></a>为模型创建表

接下来，存储模型，以便可以重新训练，也可以将其用于预测。 创建模型的 R 包的输出通常是一个**二进制对象**。 因此，可将模型存储的表必须提供的列**varbinary （max)** 类型。

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

请注意，是否第二次运行此代码，则会出现此错误：

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

以后，即可将某一模型，最后一个快速入门中，您将学习如何从其生成预测并绘制结果。

> [!div class="nextstepaction"]
> [快速入门：通过模型预测和绘图](quickstart-r-predict-from-model.md)