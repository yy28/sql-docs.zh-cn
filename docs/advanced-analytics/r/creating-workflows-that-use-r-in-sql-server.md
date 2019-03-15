---
title: 使用 R 的 SQL Server 机器学习服务创建的 SSIS 和 SSRS 的工作流
description: 结合使用 SQL Server 机器学习服务和 R Services、 Reporting Services (SSRS) 和 SQL Server Integration Services (SSIS) 的集成方案。
ms.prod: sql
ms.technology: machine-learning
ms.date: 03/15/2019
ms.topic: conceptual
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 76ddf3e3fdb43fea6bb8fd224f8199cda4134b64
ms.sourcegitcommit: e9fcd10c7eb87a4f09ac2d8f7647018e83a5f5c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2019
ms.locfileid: "57976297"
---
# <a name="create-ssis-and-ssrs-workflows-with-r-on-sql-server"></a>使用 SQL Server 上的 R 创建的 SSIS 和 SSRS 的工作流
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

此文章介绍了如何使用存储的过程在两个重要的 SQL Server 功能、 SQL Server Integration Services (SSIS) 和 SQL Server Reporting Services SSRS，将关系数据，Microsoft R 库中的数据科学函数组合在一起的方式和协调的数据转换和可视化效果的 BI 功能。 了解哪些功能的[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]同样适用于数据科学解决方案。 这篇文章还提醒你的代码和 SQL Server 上的数据，如存储过程中嵌入的 R 代码轻松使用中提供的可视化效果中[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]。

## <a name="bring-compute-power-to-the-data"></a>引入数据的计算能力

将 R 和 Python 与 SQL Server 集成的一个主要设计目标是将接近于数据分析。 这提供了多个优点：

+ 数据安全性。 与数据源将 R 更接近避免了浪费性的或不安全的数据移动。
+ 速度。 数据库针对基于集的操作进行了优化。 如内存中表的数据库的最新创新请摘要和聚合既，和是对数据科学的完美补充。
+ 易于部署和集成。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 是用于许多其他数据管理任务和应用程序的操作的中心点。 通过使用驻留在数据库或报告仓库中的数据，可以确保使用机器学习解决方案的数据是一致且最新。 
+ 跨云和本地的效率。 你可以依靠包括 [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] 和 Azure 数据工厂的企业数据管道，而非在 R 中处理数据。 可以通过 Power BI 或 [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] 轻松执行结果报告或分析。

通过恰当地组合 SQL 和 R 来执行不同的数据处理和分析任务，数据科学家和开发人员变得更加高效。

<a name="bkmk_ssis"></a> 

## <a name="use-ssis-for-data-transformation-and-automation"></a>使用 SSIS 进行数据转换和自动化

数据科学工作流具有高迭代性，并涉及许多数据转换操作，包括缩放、聚合、概率的计算，以及属性的重命名和合并。 数据科学家习惯于使用 R、Python 或其他语言执行其中许多任务，但对企业数据执行此类工作流时需要与 ETL 工具和过程无缝集成。

由于 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 支持在 R 中通过 Transact-SQL 和存储过程运行复杂的操作，因此，你可以将特定于 R 的任务与现有的 ETL 过程集成，只需执行极少的重新开发工作。 而是在 R 中执行占用大量内存的任务链，数据准备可以优化使用最高效的工具，包括[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]和[!INCLUDE[tsql](../../includes/tsql-md.md)]。 

以下是有关如何自动执行数据处理的一些观点和使用建模管道[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]:

+ 使用[!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]任务在 SQL 数据库中创建必要的数据功能
+ 使用条件分支切换 R 作业的计算上下文
+ 运行 R 作业在数据库中，生成自己的数据和共享该数据与应用程序
+ 当使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]，加载文本变量中保存的 R 脚本并在 SQL Server 中运行

## <a name="ssis-example"></a>SSIS 示例

下面的示例来自现在已停用 MSDN 博客文章作者在该 URL 的 Jimmy Wong: `https://blogs.msdn.microsoft.com/ssis/2016/01/11/operationalize-your-machine-learning-project-using-sql-server-2016-ssis-and-r-services/`。

此示例演示如何使用 SSIS 自动执行任务。 使用嵌入的 R 使用 SQL Server Management Studio，创建存储的过程，然后执行从这些存储的过程[执行 T-SQL 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)SSIS 包中。

若要单步执行此示例中，应使用 Management Studio、 SSIS，SSIS 设计器、 包设计和 T-SQL 的熟悉。 SSIS 包使用三种[执行 T-SQL 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-t-sql-statement-task)的定型数据插入表、 数据建模和评分的数据以获取预测的输出。

### <a name="create-tables"></a>创建表

若要创建的几个表的 SQL Server Management Studio 中运行以下脚本： 一个用于存储数据，另一个用于存储模型。 Ssis_iris 表的作用是充当定型数据中的操作化方案。 

```T-SQL
Use irissql
GO

Create table ssis_iris (
    id int not null identity primary key
    , "Sepal.Length" float not null, "Sepal.Width" float not null
    , "Petal.Length" float not null, "Petal.Width" float not null
    , "Species" varchar(100) null
);
GO

Create table ssis_iris_models (
    model_name varchar(30) not null default('default model') primary key,
    model varbinary(max) not null
);
GO
```

### <a name="create-a-stored-procedure-that-loads-training-data"></a>创建加载训练数据的存储的过程

此脚本创建将鸢尾花加载到数据帧中使用的内置 R 数据集的存储的过程。

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

### <a name="define-an-execute-sql-task-that-refreshes-the-model"></a>定义一个执行 SQL 任务，刷新模型

在 SSIS 设计器中，创建[执行 SQL 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)。

![将数据插入](../media/create-workflows-using-r-in-sql-server/ssis-exec-sql-insert-data.png "插入数据")

SQLStatement 的脚本如下所示。 该脚本删除现有数据，然后重新加载新数据使用**load_iris**上一步中创建存储的过程。

```T-SQL
truncate table ssis_iris;
insert into ssis_iris("Sepal.Length", "Sepal.Width", "Petal.Length", "Petal.Width", "Species")
exec dbo.load_iris;
```

### <a name="create-a-stored-procedure-that-generates-a-model"></a>创建生成的模型的存储的过程

此存储的过程是创建一个线性模型使用的代码[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)。 在 SQL Server 上的 R 和 Python 会话中自动加载 RevoScaleR 和 revoscalepy 库。

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

### <a name="define-an-execute-sql-task-that-runs-the-model-generation-stored-procedure"></a>定义运行模型生成存储的过程的执行 SQL 任务

在此步骤中，[执行 SQL 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)执行**generate_iris_rx_model**存储过程，创建模型，并将其插入到 ssis_iris_models 表。

![生成一个线性模型](../media/create-workflows-using-r-in-sql-server/ssis-exec-rxlinmod.png "生成一个线性模型")

```T-SQL
insert into ssis_iris_models (model)
exec generate_iris_rx_model;
update ssis_iris_models set model_name = 'rxLinMod' where model_name = 'default model';
```

此任务完成后，您可以查询 ssis_iris_models 以查看它包含一个二进制模型。

### <a name="predict-score-outcomes-using-the-trained-model"></a>预测 （分数） 使用"训练"的模型的结果

在此简单示例中，假定是该 ssis_iris_model 是经过训练的模型。 因为训练的模型的目的是为了生成预测，我们现在已做好运行预测使用它。 

若要执行此操作，请将 R 脚本放在要触发的 SQL 查询[rxPredict](https://docs.microsoft.com//machine-learning-server/r-reference/revoscaler/rxpredict) ssis_iris_model 上的内置 R 函数。 SQL Server 中的存储的过程调用**predict_species_length**可完成此任务。

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

### <a name="define-an-execute-sql-task-that-predicts-outcomes"></a>定义一个执行 SQL 任务，预测结果

使用[执行 SQL 任务](https://docs.microsoft.com/sql/integration-services/control-flow/execute-sql-task)，执行**predict_species_length**存储过程来生成预测的花瓣长度。

![生成预测](../media/create-workflows-using-r-in-sql-server/ssis-exec-predictions.png "生成预测")

```T-SQL
exec predict_species_length 'rxLinMod';
```

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