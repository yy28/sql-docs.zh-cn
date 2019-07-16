---
title: 从模型中使用 R 的 SQL Server 机器学习预测的快速入门
description: 在本快速入门教程，了解如何评分在 R 和 SQL Server 数据使用预构建的模型。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: 00fdcb0c8c9c535645268a0212e52eef6f7c88f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67961997"
---
# <a name="quickstart-predict-from-model-using-r-in-sql-server"></a>快速入门：从 SQL Server 中使用 R 模型预测
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

在此快速入门中，使用你创建在上一快速入门中，要针对新数据的预测评分的模型。 若要执行_评分_使用新数据，从表中，获取一个已训练模型，然后调用一组新的预测要基于的数据。 评分是一个术语，有时用于数据科学中表示生成预测、 概率或其他基于新数据送入已训练的模型的值。

## <a name="prerequisites"></a>先决条件

此快速入门，我们的扩展[创建一个预测模型](quickstart-r-create-predictive-model.md)。

## <a name="create-the-table-of-new-data"></a>创建新的数据的表

首先，创建一个表，使用新数据。 

```sql
CREATE TABLE dbo.NewMTCars(
    hp INT NOT NULL
    , wt DECIMAL(10,3) NOT NULL
    , am INT NULL
)
GO

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (110, 2.634)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (72, 3.435)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (220, 5.220)

INSERT INTO dbo.NewMTCars(hp, wt)
VALUES (120, 2.800)
GO
```

## <a name="predict-manual-transmission"></a>预测手动传输

现在，你`dbo.GLM_models`表可能包含多个 R 模型，使用不同的参数或算法，所有生成或不同的数据子集进行定型。

若要获取基于一个特定模型的预测，您必须编写执行以下 SQL 脚本：

1. 获取所需的模型
2. 获取新的输入数据
3. 调用与该模型兼容的 R 预测函数

在此示例中，我们将使用名为的模型`default model`。

```sql
DECLARE @glmmodel varbinary(max) = 
    (SELECT model FROM dbo.GLM_models WHERE model_name = 'default model');

EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(glmmodel));
            new <- data.frame(NewMTCars);
            predicted.am <- predict(current_model, new, type = "response");
            str(predicted.am);
            OutputDataSet <- cbind(new, predicted.am);
            '
    , @input_data_1 = N'SELECT hp, wt FROM dbo.NewMTCars'
    , @input_data_1_name = N'NewMTCars'
    , @params = N'@glmmodel varbinary(max)'
    , @glmmodel = @glmmodel
WITH RESULT SETS ((new_hp INT, new_wt DECIMAL(10,3), predicted_am DECIMAL(10,3)));
```

上述脚本将执行以下步骤：

+ 使用 SELECT 语句从表中获取单个模型，并将它作为输入参数传递。

+ 从表中检索模型后，针对该模型调用 `unserialize` 函数。

+ 将带有相应参数的 `predict` 函数应用到该模型，并提供新的输入数据。

+ 在示例中，`str`函数添加在测试阶段，以检查从 R.返回的数据架构您可以删除的语句更高版本。

+ 在 R 脚本中使用的列名称不一定被传递给存储的过程输出中。 此处我们使用了 WITH RESULTS 子句来定义一些新的列名称。

**结果**

![结果集进行预测 properbility 手动传输](./media/r-predict-am-resultset.png)

它也是可以使用[在 TRANSACT-SQL 中的 PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql)生成预测的值或基于存储模型的分数。

## <a name="next-steps"></a>后续步骤

将 R 与 SQL Server 集成后，可以更方便地大规模部署 R 解决方案，利用 R 和关系数据库的最佳功能实现高性能数据处理和快速 R 分析。 

继续学习如何使用 R 和 SQL Server 通过由 Microsoft 数据科学和 R Services 开发团队创建的端到端方案的解决方案。

> [!div class="nextstepaction"]
> [SQL Server R 教程](sql-server-r-tutorials.md)
