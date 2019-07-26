---
title: 使用 R 从模型预测快速入门
description: 在本快速入门中, 了解如何使用 R 中的预构建模型和 SQL Server 的数据进行评分。
ms.prod: sql
ms.technology: machine-learning
ms.date: 01/04/2019
ms.topic: quickstart
author: dphansen
ms.author: davidph
ms.openlocfilehash: aa3a65020f2900bc4d9e0b5c5fd5a200f3334435
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469339"
---
# <a name="quickstart-predict-from-model-using-r-in-sql-server"></a>快速入门：在 SQL Server 中使用 R 预测模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入门中, 请使用在前面的快速入门中创建的模型来对新数据进行评分。 若要使用新数据执行_评分_, 请从表中获取一个定型模型, 然后调用一组要对其进行预测的新数据。 评分是一种术语, 这种术语有时在数据科学中使用, 以根据送入定型模型的新数据来生成预测、概率或其他值。

## <a name="prerequisites"></a>先决条件

此快速入门是[创建预测模型](quickstart-r-create-predictive-model.md)的扩展。

## <a name="create-the-table-of-new-data"></a>创建新数据表

首先, 使用新数据创建一个表。 

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

现在, `dbo.GLM_models`表可能包含多个 R 模型、使用不同的参数或算法生成, 或在不同的数据子集上定型。

若要获取基于某个特定模型的预测, 必须编写执行以下操作的 SQL 脚本:

1. 获取所需的模型
2. 获取新的输入数据
3. 调用与该模型兼容的 R 预测函数

在此示例中, 我们将使用名为`default model`的模型。

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

上述脚本执行以下步骤:

+ 使用 SELECT 语句从表中获取单个模型，并将它作为输入参数传递。

+ 从表中检索模型后，针对该模型调用 `unserialize` 函数。

+ 将带有相应参数的 `predict` 函数应用到该模型，并提供新的输入数据。

+ 在此示例中, `str`在测试阶段添加了函数, 以检查从 R 返回的数据的架构。稍后可以删除该语句。

+ R 脚本中使用的列名不必传递到存储过程输出。 这里, 我们使用了 WITH RESULTS 子句定义了一些新的列名。

**结果**

![用于预测手动传输 properbility 的结果集](./media/r-predict-am-resultset.png)

还可以在[transact-sql 中使用 PREDICT](https://docs.microsoft.com/sql/t-sql/queries/predict-transact-sql) , 根据存储的模型生成预测值或分数。

## <a name="next-steps"></a>后续步骤

将 R 与 SQL Server 集成后，可以更方便地大规模部署 R 解决方案，利用 R 和关系数据库的最佳功能实现高性能数据处理和快速 R 分析。 

继续了解通过 Microsoft 数据科学和 R 服务开发团队创建的端到端方案, 使用 R 与 SQL Server 的解决方案。

> [!div class="nextstepaction"]
> [SQL Server R 教程](sql-server-r-tutorials.md)
