---
title: 在 R 中创建和评分预测模型
titleSuffix: SQL Server Machine Learning Services
description: 使用 SQL Server 机器学习服务在 R 中创建一个简单的预测模型，然后使用新数据预测结果。
ms.prod: sql
ms.technology: machine-learning
ms.date: 10/04/2019
ms.topic: quickstart
author: garyericson
ms.author: garye
ms.reviewer: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: fc968c9364f23826b366721590f72ac1b0af0391
ms.sourcegitcommit: 454270de64347db917ebe41c081128bd17194d73
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72005976"
---
# <a name="quickstart-create-and-score-a-predictive-model-in-r-with-sql-server-machine-learning-services"></a>快速入门：使用 SQL Server 机器学习服务创建和评分预测模型
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

在本快速入门中，你将使用 R 创建和训练预测模型，将该模型保存到 SQL Server 实例中的表，然后使用该模型从使用[SQL Server 机器学习服务](../what-is-sql-server-machine-learning.md)的新数据中预测值。

您将在本快速入门中使用的模型是一个简单的通用线性模型（GLM），该模型预测车辆经过手动传输的概率。 你将使用 R 附带的**mtcars**数据集。

> [!TIP]
> 如果需要针对线性模型的刷新器，请尝试本教程，其中介绍了使用 rxLinMod 对模型进行调整的过程：[Fitting Linear Models](/machine-learning-server/r/how-to-revoscaler-linear-model)（拟合线性模型）

## <a name="prerequisites"></a>先决条件

- 此快速入门要求使用安装 R 语言的[SQL Server 机器学习服务](../install/sql-machine-learning-services-windows-install.md)SQL Server 的实例。

  SQL Server 实例可位于 Azure 虚拟机或本地。 请注意，默认情况下禁用外部脚本功能，因此在开始之前，您可能需要[启用外部脚本](../install/sql-machine-learning-services-windows-install.md#bkmk_enableFeature)并验证**SQL Server Launchpad 服务**是否正在运行。

- 还需要一个用于运行包含 R 脚本的 SQL 查询的工具。 您可以使用任何数据库管理或查询工具运行这些脚本，只要它可以连接到 SQL Server 实例，然后运行 T-sql 查询或存储过程。 本快速入门使用[SQL Server Management Studio （SSMS）](https://docs.microsoft.com/sql/ssms/sql-server-management-studio-ssms)。

## <a name="create-the-model"></a>创建模型

若要创建模型，你将创建用于定型的源数据，创建模型并使用数据进行定型，然后将该模型存储在 SQL 数据库中，该数据库可用于生成包含新数据的预测。

### <a name="create-the-source-data"></a>创建源数据

1. 打开**SQL Server Management Studio** ，然后连接到 SQL Server 实例。

1. 创建一个表以保存训练数据。

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

1. 插入内置数据集中的数据 `mtcars`。

   ```SQL
   INSERT INTO dbo.MTCars
   EXEC sp_execute_external_script @language = N'R'
       , @script = N'MTCars <- mtcars;'
       , @input_data_1 = N''
       , @output_data_1_name = N'MTCars';
   ```

   > [!TIP]
   > R 运行时包含许多或大或小的数据集。 若要获取随 R 一起安装的数据集列表，请在 R 命令提示符下键入 `library(help="datasets")`。

### <a name="create-and-train-the-model"></a>创建和训练模型

Car 速度数据包含两列：数字：动力（`hp`）和权重（`wt`）。 在此数据中，你将创建一个通用线性模型（GLM），该模型会估算车辆已调整为手动传输的概率。

若要生成模型，请在 R 代码中定义公式，并将数据作为输入参数传递。

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

- @No__t 的第一个参数是*公式*参数，它将 `am` 定义为依赖于 @no__t 3。
- 输入数据存储在 SQL 查询填充的变量 `MTCarsData` 中。 如果未将特定的名称分配到输入数据，默认变量名称将是 _InputDataSet_。

### <a name="store-the-model-in-the-sql-database"></a>在 SQL 数据库中存储模型

接下来，将模型存储在 SQL 数据库中，以便可以使用它进行预测或重新训练。 

1. 创建一个表来存储模型。

   创建模型的 R 包的输出通常是一个二进制对象。 因此，存储模型的表必须提供**varbinary （max）** 类型的列。

   ```sql
   CREATE TABLE GLM_models (
       model_name varchar(30) not null default('default model') primary key,
       model varbinary(max) not null
   );
   ```

1. 运行下面的 Transact-sql 语句以调用存储过程，生成模型并将其保存到所创建的表中。

   ```sql
   INSERT INTO GLM_models(model)
   EXEC generate_GLM;
   ```

   > [!TIP]
   > 如果第二次运行此代码，将收到此错误："PRIMARY KEY 约束冲突 ...无法在对象 stopping_distance_models "中插入重复键。 避免此错误的一种做法是更新每个新模型的名称。 例如，可将该名称更改为更具描述性的名称，并包含模型类型、创建日期，等等。

     ```sql
     UPDATE GLM_models
     SET model_name = 'GLM_' + format(getdate(), 'yyyy.MM.HH.mm', 'en-gb')
     WHERE model_name = 'default model'
     ```

## <a name="score-new-data-using-the-trained-model"></a>使用定型模型对新数据进行评分

*评分*是一种术语，用于根据馈送到定型模型中的新数据来生成预测、概率或其他值。 您将使用在上一节中创建的模型来对新数据进行评分。

### <a name="create-a-table-of-new-data"></a>创建新数据表

首先，使用新数据创建一个表。

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

### <a name="predict-manual-transmission"></a>预测手动传输

若要根据模型获取预测，请编写一个执行以下操作的 SQL 脚本：

1. 获取所需的模型
1. 获取新的输入数据
1. 调用与该模型兼容的 R 预测函数

随着时间的推移，表可能包含多个 R 模型、使用不同的参数或算法生成，或在不同的数据子集上定型。 在此示例中，我们将使用名为 `default model` 的模型。

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

上述脚本执行以下步骤：

- 使用 SELECT 语句从表中获取单个模型，并将它作为输入参数传递。

- 从表中检索模型后，针对该模型调用 `unserialize` 函数。

- 将带有相应参数的 `predict` 函数应用到该模型，并提供新的输入数据。

> [!NOTE]
> 在此示例中，在测试阶段添加了 `str` 函数，以检查从 R 返回的数据的架构。稍后可以删除该语句。
>
> R 脚本中使用的列名不必传递到存储过程输出。 此处使用 WITH RESULTS 子句来定义一些新的列名。

**结果**

![用于预测手动传输 properbility 的结果集](./media/r-predict-am-resultset.png)

还可以使用[PREDICT （transact-sql）](../../t-sql/queries/predict-transact-sql.md)语句基于存储的模型生成预测值或分数。

## <a name="next-steps"></a>后续步骤

有关 SQL Server 机器学习服务的详细信息，请参阅：

- [什么是 SQL Server 机器学习服务（Python 和 R）？](../what-is-sql-server-machine-learning.md)
