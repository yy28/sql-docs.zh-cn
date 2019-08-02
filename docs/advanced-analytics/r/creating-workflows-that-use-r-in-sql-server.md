---
title: 使用 R 创建 SSIS 和 SSRS 工作流
description: 集成方案将 SQL Server 机器学习服务和 R Services、Reporting Services (SSRS) 和 SQL Server Integration Services (SSIS) 结合在一起。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: 2b8d55e95991437e4d76911fd26afb5b1bc9c550
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68715175"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>在 SQL Server 上通过 R 创建 SSIS 和 SSRS 工作流
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本文介绍如何使用具有两个重要 SQL Server 功能的 SQL Server 机器学习服务的语言和数据科学功能来使用嵌入的 R 和 Python 脚本:SQL Server Integration Services (SSIS) 和 SQL Server Reporting Services SSRS。 SQL Server 中的 R 和 Python 库提供了统计和预测功能。 SSIS 和 SSRS 分别提供协调的 ETL 转换和可视化。 本文介绍如何在此工作流模式中将所有这些功能组合在一起:

> [!div class="checklist"]
> * 创建包含可执行 R 或 Python 的存储过程
> * 从 SSIS 或 SSRS 执行存储过程

本文中的示例主要介绍 R 和 SSIS, 但概念和步骤同样适用于 Python。 第二部分提供了适用于 SSRS 可视化的指南和链接。

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-automation"></a>将 SSIS 用于自动化

数据科学工作流具有高迭代性，并涉及许多数据转换操作，包括缩放、聚合、概率的计算，以及属性的重命名和合并。 数据科学家习惯于使用 R、Python 或其他语言执行其中许多任务，但对企业数据执行此类工作流时需要与 ETL 工具和过程无缝集成。

由于[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]使你可以通过 transact-sql 和存储过程在 R 中运行复杂的操作, 因此你可以将数据科学任务与现有的 ETL 过程集成在一起。 数据准备可以使用最有效的工具 (包括[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和[!INCLUDE[tsql](../../includes/tsql-md.md)]) 进行优化, 而不是执行内存密集型任务链。 

下面是有关如何使用[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]自动执行数据处理和建模管道的一些建议:

+ 从本地或云源提取数据以生成定型数据 
+ 构建和运行 R 或 Python 模型作为数据集成工作流的一部分
+ 定期 (计划) 重新训练模型
+ 将 R 或 Python 脚本的结果加载到其他目标 (如 Excel、Power BI、Oracle 和 Teradata), 以将其命名为一些
+ 使用 SSIS 任务在 SQL 数据库中创建数据功能
+ 使用条件分支切换 R 和 Python 作业的计算上下文

## <a name="ssis-example"></a>SSIS 示例

以下示例源自现已停用的 MSDN 博客文章, 此文章由 Jimmy Wong 在此 URL 中创作:`https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`

此示例演示如何使用 SSIS 自动执行任务。 使用 SQL Server Management Studio 创建使用嵌入 R 的存储过程, 然后从 SSIS 包中的 "[执行 t-sql 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)" 执行这些存储过程。

若要单步执行此示例, 应熟悉 Management Studio、SSIS、SSIS 设计器、包设计和 T-sql。 SSIS 包使用三个[执行 t-sql 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task), 这些任务将定型数据插入到表中, 对数据进行建模, 并对数据进行评分以获取预测输出。

### <a name="load-training-data"></a>加载定型数据

在 SQL Server Management Studio 中运行以下脚本, 以创建用于存储数据的表。 在此练习中, 应创建并使用测试数据库。 

```T-SQL
Use test-db
GO

Create table ssis_iris (
    id int not null identity primary key
    , "Sepal.Length" float not null, "Sepal.Width" float not null
    , "Petal.Length" float not null, "Petal.Width" float not null
    , "Species" varchar(100) null
);
GO
```

创建将定型数据加载到数据帧的存储过程。 此示例使用的是内置的 Iris 数据集。 

```T-SQL
Create procedure load_iris
as
begin
    execute sp_execute_external_script
        @language = N'R'
        , @script = N'iris_df <- iris;'
        , @input_data_1 = N''
        , @output_data_1_name = N'iris_df'
    with result sets (("Sepal.Length" float not null, "Sepal.Width" float not null, "Petal.Length" float not null, "Petal.Width" float not null, "Species" varchar(100)));
end;
```

在 SSIS 设计器中, 创建执行您刚定义的存储过程的[执行 SQL 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)。 **SQLStatement**的脚本将删除现有数据, 指定要插入的数据, 然后调用存储过程来提供数据。

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

![插入数据](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "插入数据")

### <a name="generate-a-model"></a>生成模型

在 SQL Server Management Studio 中运行以下脚本, 以创建存储模型的表。 

```T-SQL
Use test-db
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

使用[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)创建用于生成线性模型的存储过程。 RevoScaleR 和 revoscalepy 库在 SQL Server 上自动提供 R 和 Python 会话, 因此无需导入库。

```T-SQL
Create procedure generate_iris_rx_model
as
begin
    execute sp_execute_external_script
        @language = N'R'
        , @script = N'
          irisLinMod <- rxLinMod(Sepal.Length ~ Sepal.Width + Petal.Length + Petal.Width + Species, data = ssis_iris);
          trained_model <- data.frame(payload = as.raw(serialize(irisLinMod, connection=NULL)));'
        , @input_data_1 = N'select "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from ssis_iris'
        , @input_data_1_name = N'ssis_iris'
        , @output_data_1_name = N'trained_model'
    with result sets ((model varbinary(max)));
end;
GO
```

在 SSIS 设计器中, 创建[执行 SQL 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)以执行**generate_iris_rx_model**存储过程。 模型被序列化并保存到 ssis_iris_models 表中。 **SQLStatement**的脚本如下所示:

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

![生成线性模型](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "生成线性模型")

作为检查点, 在此任务完成后, 可以查询 ssis_iris_models 以查看它是否包含一个二进制模型。

### <a name="predict-score-outcomes-using-the-trained-model"></a>使用 "定型" 模型预测 (评分) 结果

现在, 您已经有了用于加载定型数据并生成模型的代码, 但唯一的步骤是使用模型来生成预测。 

为此, 请在 SQL 查询中放置 R 脚本, 以触发 ssis_iris_model 上的[rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict)内置 R 函数。 称为**predict_species_length**的存储过程完成此任务。

```T-SQL
Create procedure predict_species_length (@model varchar(100))
as
begin
    declare @rx_model varbinary(max) = (select model from ssis_iris_models where model_name = @model);
    -- Predict based on the specified model:
    exec sp_execute_external_script
        @language = N'R'
        , @script = N'
irismodel <-unserialize(rx_model);
irispred <- rxPredict(irismodel, ssis_iris[,2:6]);
OutputDataSet <- cbind(ssis_iris[1], irispred$Sepal.Length_Pred, ssis_iris[2]);
colnames(OutputDataSet) <- c("id", "Sepal.Length.Actual", "Sepal.Length.Expected");
#OutputDataSet <- subset(OutputDataSet, Species.Length.Actual != Species.Expected);
'
    , @input_data_1 = N'
    select id, "Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species" from ssis_iris
    '
    , @input_data_1_name = N'ssis_iris'
    , @params = N'@rx_model varbinary(max)'
    , @rx_model = @rx_model
    with result sets ( ("id" int, "Species.Length.Actual" float, "Species.Length.Expected" float)
        );
end;
```

在 SSIS 设计器中, 创建执行**predict_species_length**存储过程以生成预测花瓣长度的[执行 SQL 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)。

```T-SQL
exec predict_species_length 'rxLinMod';
```

![生成预测](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "生成预测")

### <a name="run-the-solution"></a>运行解决方案

在 SSIS 设计器中, 按 F5 以执行包。 应会看到类似于以下屏幕截图的结果。

![按 F5 在调试模式下运行](../media/create-workflows-using-r-in-sql-server/ssis-exec-F5-run.png "按 F5 在调试模式下运行")

<a name="bkmk_ssrs"></a> 

## <a name="use-ssrs-for-visualizations"></a>使用 SSRS 进行可视化

虽然 R 可以创建图表和有趣的可视化效果, 但它不会与外部数据源进行良好集成, 这意味着必须单独生成每个图表或图形。 共享可能也比较困难。

通过使用[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], 你可以在 R 中通过[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程运行复杂的操作, 这些操作很容易由各种企业报告工具 (包括[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 Power BI) 使用。

### <a name="ssrs-example"></a>SSRS 示例

[用于 Microsoft Reporting Services (SSRS) 的R Graphics Device](https://rgraphicsdevice.codeplex.com/)

此 CodePlex 项目提供的代码可帮助你创建自定义报表项, 以将 R 的图形输出呈现为可在报表中[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]使用的图像。  通过使用自定义报表，你可以：

+ 将使用 R Graphics Device 创建的图表和绘图发布到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 仪表板

+ 将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 参数传递到 R 绘图

> [!NOTE]
> 对于本示例, 必须在 Reporting Services 服务器以及 Visual Studio 中安装支持 R 图形设备用于 Reporting Services 的代码。 还需要进行手动编译和配置。

## <a name="next-steps"></a>后续步骤

本文中的 SSIS 和 SSRS 示例说明了执行包含嵌入式 R 或 Python 脚本的存储过程的两种情况。 关键的要点在于是, 可以使 R 或 Python 脚本可用于可在存储过程中发送执行请求的任何应用程序或工具。 SSIS 的另一个要点在于是, 可以创建包来自动执行和计划各种操作, 如数据采集、清理、操作等, 以及操作链中包含的 R 或 Python 数据科学功能。 有关详细信息和想法, 请参阅[SQL Server 机器学习服务中使用存储过程的操作 R 代码](operationalizing-your-r-code.md)。