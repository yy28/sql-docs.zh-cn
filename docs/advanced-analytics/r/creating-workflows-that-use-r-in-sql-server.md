---
title: 使用 R 的 SQL Server 机器学习服务创建的 SSIS 和 SSRS 的工作流
description: 结合使用 SQL Server 机器学习服务和 R Services、 Reporting Services (SSRS) 和 SQL Server Integration Services (SSIS) 的集成方案。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/17/2019
ms.topic: conceptual
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 5d480b7cd24200b051fa2626fc41fa757703eaf8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62642631"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>使用 SQL Server 上的 R 创建的 SSIS 和 SSRS 的工作流
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文介绍了如何使用嵌入的 R 和 Python 脚本与两个重要的 SQL Server 功能配合使用的 SQL Server 机器学习服务的语言和数据科学功能：SQL Server Integration Services (SSIS) 和 SQL Server Reporting Services SSRS。 SQL Server 中的 R 和 Python 库提供的统计和预测函数。 SSIS 和 SSRS 分别提供协调 ETL 转换和可视化效果。 本文介绍了如何将所有这些功能一起放在此模式下工作流：

> [!div class="checklist"]
> * 创建包含可执行的 R 或 Python 的存储的过程
> * 从 SSIS 或 SSRS 执行存储的过程

这篇文章中的示例是主要是关于 R 和 SSIS，但概念和步骤同样适用于 Python。 第二个部分提供 SSRS 可视化效果的指导和链接。

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-automation"></a>使用 SSIS 实现自动化

数据科学工作流具有高迭代性，并涉及许多数据转换操作，包括缩放、聚合、概率的计算，以及属性的重命名和合并。 数据科学家习惯于使用 R、Python 或其他语言执行其中许多任务，但对企业数据执行此类工作流时需要与 ETL 工具和过程无缝集成。

因为[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，可在 R 中通过 TRANSACT-SQL 和存储的过程运行复杂的操作可以将数据科学任务与现有的 ETL 过程集成。 而是执行占用大量内存的任务链，数据准备可以优化使用最高效的工具，包括[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和[!INCLUDE[tsql](../../includes/tsql-md.md)]。 

以下是有关如何自动执行数据处理的一些观点和使用建模管道[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ 提取数据从本地或云源来生成训练数据 
+ 生成并运行 R 或 Python 模型作为数据集成工作流的一部分
+ （已计划） 定期重新定型
+ 从 R 或 Python 脚本的结果加载到 Excel、 Power BI、 Oracle 和 Teradata，仅举几例等其他目标
+ 使用 SSIS 任务在 SQL 数据库中创建数据功能
+ 使用条件分支切换 R 和 Python 的作业的计算上下文

## <a name="ssis-example"></a>SSIS 示例

下面的示例来自作者在该 URL 的 Jimmy Wong 现在已停用 MSDN 博客文章： `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`

此示例演示如何使用 SSIS 自动执行任务。 使用嵌入的 R 使用 SQL Server Management Studio，创建存储的过程，然后执行从这些存储的过程[执行 T-SQL 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)SSIS 包中。

若要单步执行此示例中，应使用 Management Studio、 SSIS，SSIS 设计器、 包设计和 T-SQL 的熟悉。 SSIS 包使用三种[执行 T-SQL 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)的定型数据插入表、 数据建模和评分的数据以获取预测的输出。

### <a name="load-training-data"></a>加载训练数据

若要创建用于存储数据的表的 SQL Server Management Studio 中运行以下脚本。 应创建并测试数据库用于此练习。 

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

创建存储的过程，将训练数据加载到数据帧。 此示例中使用内置的鸢尾花数据集。 

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

在 SSIS 设计器中，创建[执行 SQL 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)执行存储的过程只需定义。 有关脚本**SQLStatement**删除现有数据，则指定要插入的数据，然后调用存储的过程提供的数据。

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

![将数据插入](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "插入数据")

### <a name="generate-a-model"></a>生成模型

若要创建存储模型的表的 SQL Server Management Studio 中运行以下脚本。 

```T-SQL
Use test-db
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

创建生成线性模型使用的存储的过程[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)。 RevoScaleR 和 revoscalepy 库是在 SQL Server 上的 R 和 Python 会话中自动可用，因此无需将库导入。

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

在 SSIS 设计器中，创建[执行 SQL 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)执行**generate_iris_rx_model**存储过程。 序列化模型并将其保存到 ssis_iris_models 表中。 有关脚本**SQLStatement**如下所示：

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

![生成一个线性模型](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "生成一个线性模型")

作为一个检查点，此任务完成后，您可以查询 ssis_iris_models 以查看它包含一个二进制模型。

### <a name="predict-score-outcomes-using-the-trained-model"></a>预测 （分数） 使用"训练"的模型的结果

现在，您的代码加载训练数据和生成的模型，剩余的唯一步骤使用模型来生成预测。 

若要执行此操作，请将 R 脚本放在要触发的 SQL 查询[rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) ssis_iris_model 上的内置 R 函数。 调用存储的过程**predict_species_length**可完成此任务。

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

在 SSIS 设计器中，创建[执行 SQL 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)执行**predict_species_length**存储过程来生成预测的花瓣长度。

```T-SQL
exec predict_species_length 'rxLinMod';
```

![生成预测](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "生成预测")

### <a name="run-the-solution"></a>运行解决方案

在 SSIS 设计器中，按 F5 执行包。 应会看到结果类似于以下屏幕截图。

![F5 在调试模式下运行](../media/create-workflows-using-r-in-sql-server/ssis-exec-F5-run.png "F5 在调试模式下运行")

<a name="bkmk_ssrs"></a> 

## <a name="use-ssrs-for-visualizations"></a>SSRS 用于可视化效果

虽然 R 可以创建图表和有趣的可视化效果，但并不与外部数据源，这意味着，每个图表或图形必须单独生成了良好的集成。 共享可能也比较困难。

通过使用[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]，可以在 R 中通过运行复杂的操作[!INCLUDE[tsql](../../includes/tsql-md.md)]存储过程，通过各种企业报告工具，包括可以轻松使用[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]和 Power BI。

### <a name="ssrs-example"></a>SSRS 示例

[用于 Microsoft Reporting Services (SSRS) 的R Graphics Device](https://rgraphicsdevice.codeplex.com/)

此 CodePlex 项目提供了可帮助您创建自定义报表项的代码将 R 的图形输出呈现为可以使用中的图像[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]报表。  通过使用自定义报表，你可以：

+ 将使用 R Graphics Device 创建的图表和绘图发布到 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 仪表板

+ 将 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 参数传递到 R 绘图

> [!NOTE]
> 对于此示例，在 Reporting Services 服务器上，以及 Visual Studio 中，必须安装支持的 Reporting Services 的 R Graphics Device 的代码。 还需要进行手动编译和配置。

## <a name="next-steps"></a>后续步骤

在本文中的 SSIS 和 SSRS 示例演示了执行包含嵌入的 R 或 Python 脚本的存储的过程的两种情况。 关键的一点是，您可以将 R 或 Python 脚本提供到任何应用程序或工具都可以对存储过程发送执行请求。 SSIS 的其他要点在于，可以创建自动执行和计划的各种操作，如数据采集、 清理、 操作和等，R 或 Python 数据科学功能操作链中包含的包。 有关详细信息和观点，请参阅[操作 R 代码在 SQL Server 机器学习服务中使用存储的过程](operationalizing-your-r-code.md)。