---
title: 预测和绘制从模型 (SQL 快速入门中的 R) |Microsoft 文档
ms.custom: ''
ms.date: 08/20/2017
ms.reviewer: ''
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: tutorial
dev_langs:
- R
- SQL
ms.author: heidist
author: HeidiSteen
manager: cgronlun
ms.workload: On Demand
ms.openlocfilehash: b30c2443b8b1532d008e717e1b86fdb62adbe0a1
ms.sourcegitcommit: 059fc64ba858ea2adaad2db39f306a8bff9649c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/04/2018
---
# <a name="predict-and-plot-from-model-r-in-sql-quickstart"></a>预测和绘制从模型 (SQL 快速入门中的 R)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

若要执行_评分_使用新数据，从表中获取训练的模型之一，然后调用一组新的基于预测的数据。 计分就是一个术语，有时用于数据科学中表示生成预测、 概率或基于送入训练的模型的新数据的其他值。

## <a name="create-the-table-of-new-speeds"></a>创建新速度表

你是否注意到，原始训练数据在每小时 25 英里的速度处就不再继续了？ 这是因为原始数据基于 1920 年的试验！

你可能想要知道，假设 20 世纪 20 年代的汽车能够跑到 60 甚至 100 mph，那么停止下来需要花费多长时间？ 若要回答这个问题，必须提供一些新的速度值。

```sql
CREATE TABLE [dbo].[NewCarSpeed]([speed] [int] NOT NULL,
    [distance] [int]  NULL) ON [PRIMARY]
GO
INSERT [dbo].[NewCarSpeed] (speed)
VALUES (40),  (50),  (60), (70), (80), (90), (100)
```

## <a name="predict-stopping-distance"></a>预测停止距离

目前，表中可能包含多个 R 模型，其中的所有模型都是使用不同的参数或算法构建的，或者已根据不同的数据子集进行训练。

![rsql_basictut_listofmodels](media/rsql-basictut-listofmodels.png)

若要获取基于一个特定模型的预测，你必须编写将执行以下 SQL 脚本：

1. 获取所需的模型
2. 获取新的输入数据
3. 调用与该模型兼容的 R 预测函数

在此示例中，因为您的模型基于**rxLinMod**作为的一部分提供的算法**RevoScaleR**调用的包， [rxPredict](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxpredict)函数，而不是泛型 R`predict`函数。

```sql
DECLARE @speedmodel varbinary(max) = (SELECT model FROM [dbo].[stopping_distance_models] WHERE model_name = 'latest model');
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(speedmodel));
            new <- data.frame(NewCarData);
            predicted.distance <- rxPredict(current_model, new);
            str(predicted.distance);
            OutputDataSet <- cbind(new, ceiling(predicted.distance));
            '
    , @input_data_1 = N' SELECT speed FROM [dbo].[NewCarSpeed] '
    , @input_data_1_name = N'NewCarData'
    , @params = N'@speedmodel varbinary(max)'
    , @speedmodel = @speedmodel
WITH RESULT SETS (([new_speed] INT, [predicted_distance] INT))
```

+ 使用 SELECT 语句从表中获取单个模型，并将它作为输入参数传递。
+  从表中检索模型后，针对该模型调用 `unserialize` 函数。

    > [!TIP] 
    > 此外签出新[序列化函数](https://docs.microsoft.com/r-server/r-reference/revoscaler/rxserializemodel)支持由 RevoScaleR，[实时评分](../../advanced-analytics/real-time-scoring.md)。
+  将带有相应参数的 `rxPredict` 函数应用到该模型，并提供新的输入数据。
+  在示例中，`str`函数添加在测试阶段，检查正在从。 返回的数据的架构你可以删除该语句。
+ 在 R 脚本中使用的列名称不一定传递给存储的过程输出中。 此处我们已使用与结果子句来定义一些新的列名称。

**结果**

![rsql_basictut_scoringresults_smalldata](media/rsql-basictut-scoringresults-smalldata.PNG)

## <a name="perform-scoring-in-parallel"></a>并行执行评分

对于这个微小的数据集，很快就返回了预测结果。 但是，如何快速做出大量预测？ 有多种方法来加快操作的 SQL Server 中更因此如果的操作可以并行处理。 具体而言，对于评分，一种简单的方式是将 *@parallel* 参数添加到 `sp_execute_external_script`，并将值设置为 **1**。

假设你已获取一个大得多的可能车速表，其中包含几十万个值。 社区提供的许多示例 T-SQL 脚本可帮助你生成数据表，本文不会重新生成这些表。 假设某个列包含多个整数，你想要使用该列作为模型中 `speed` 的输入。

若要执行此操作，只需运行相同的预测查询中，但替换更大的数据集，并添加`@parallel = 1`自变量。

```sql
DECLARE @speedmodel varbinary(max) = (select model from [dbo].[stopping_distance_models] where model_name = 'default model');
EXEC sp_execute_external_script
    @language = N'R'
    , @script = N'
            current_model <- unserialize(as.raw(speedmodel));
            new <- data.frame(NewCarData);
            predicted.distance <- rxPredict(current_model, new);
            OutputDataSet <- cbind(new, ceiling(predicted.distance));
            '
    , @input_data_1 = N' SELECT [speed] FROM [dbo].[HugeTableofCarSpeeds] '
    , @input_data_1_name = N'NewCarData'
    , @parallel = 1
    , @params = N'@speedmodel varbinary(max)'
    , @speedmodel = @speedmodel
WITH RESULT SETS (([new_speed] INT, [predicted_distance] INT))
```

+ 仅当使用非常大的数据时，并行执行通常提供好处。 SQL 数据库引擎可能会决定不需要并行执行。 此外，获取数据的 SQL 查询必须能够生成并行查询计划。

+ 使用并行执行的选项时，**必须**提前使用 WITH RESULT SETS 子句指定输出结果架构。 提前指定输出架构可睛 SQL Server 聚合多个并行数据集，否则可能会生成未知的架构。

+ 如果你是*培训*的模型，而不是*评分*，此参数通常不会产生影响。 根据模型类型，创建模型过程可能需要在读取所有行之后才能创建摘要。

+ 若要获取的并行处理时模型定型的优势，我们建议你使用之一**RevoScaleR**算法。 这些算法用于分发处理将自动，即使未指定<code>@parallel =1</code>对的调用中`sp_execute_external_script`。 有关如何获取与 RevoScaleR 算法的最佳性能的指南，请参阅[分布式和并行计算与 Microsoft R 中 ScaleR](https://docs.microsoft.com/r-server/r/how-to-revoscaler-distributed-computing)。

## <a name="create-an-r-plot-of-the-model"></a>创建模型的 R 绘图

许多客户端（包括 SQL Server Management Studio）无法直接显示使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 创建的绘图。 相反，生成 R 图形的一般过程是创建为 R 代码的一部分的绘图，然后将映像写入到文件。

或者，你可以返回的任何应用程序可以显示图像的序列化的二进制绘图对象。

以下示例演示如何使用 R 默认包含的绘图功能创建一个简单图形。该图像将输出到指定的文件，同时由存储过程输出到某个 SQL 变量。

```sql
 EXECUTE sp_execute_external_script
 @language = N'R'
 , @script = N'
     imageDir <- ''C:\\temp\\plots'';
     image_filename = tempfile(pattern = "plot_", tmpdir = imageDir, fileext = ".jpg")
     print(image_filename);
     jpeg(filename=image_filename,  width=600, height = 800);
     print(plot(distance~speed, data=InputDataSet, xlab="Speed", ylab="Stopping distance", main = "1920 Car Safety"));
     abline(lm(distance~speed, data = InputDataSet));
     dev.off();
     OutputDataSet <- data.frame(data=readBin(file(image_filename, "rb"), what=raw(), n=1e6));
     '
  , @input_data_1 = N'SELECT speed, distance from [dbo].[CarSpeed]'
  WITH RESULT SETS ((plot varbinary(max)));
```

+ `tempfile`函数将返回字符串可用作文件名，但尚未生成该文件。
+ 参数`tempfile`，你可以指定前缀和文件扩展名，以及目录。 若要验证的完整文件名和路径，打印消息使用`str()`。
+ `jpeg` 函数使用指定的参数创建 R 设备。
+ 创建该绘图后，你可以向其添加更多的可视化功能。 在这种情况下，使用添加的回归线`abline`。
+ 添加完绘图特征后，必须使用 `dev.off()` 函数关闭图形设备。
+ `readBin` 函数使用要读取的文件、格式规范以及记录数。 `rb`* * 的关键字表示该文件是二进制而不是文本。

**结果**

![rsql_basictut_plotresult_small](media/rsql-basictut-plotresult-small.png)

如果想要使用 R 的某些强大图形包创建更复杂的绘图，我们建议阅读以下文章。 在这两篇文章中，都需要使用流行的 **ggplot2** 包。

+ [Loan Classification using SQL Server 2016 R Services](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/09/27/loan-classification-using-sql-server-2016-r-services/)（使用 SQL Server 2016 R Services 进行借贷分类）基于保险数据的端到端方案。 需要**重塑**包。
+ [创建关系图和使用 R 的图形](../../advanced-analytics/tutorials/walkthrough-create-graphs-and-plots-using-r.md)

## <a name="conclusions"></a>结论

将 R 与 SQL Server 集成后，可以更方便地大规模部署 R 解决方案，利用 R 和关系数据库的最佳功能实现高性能数据处理和快速 R 分析。 

请参阅这些其他资源的更多 R 示例：

+  [SQL Server R 教程](../../advanced-analytics/tutorials/sql-server-r-tutorials.md)

    继续了解 R 使用 SQL Server，通过创建了 Microsoft 数据科学和 R Services 开发团队的端到端方案的解决方案。

+ [SQL Server Python 教程](../../advanced-analytics/tutorials/sql-server-python-tutorials.md)

    为 SQL Server 自 2017 年，使用的 Python 语言远程计算上下文和可扩展的算法的能力。

+ [教程和 Microsoft R 的示例数据](https://docs.microsoft.com/r-server/r/tutorial-introduction)

    了解如何使用新的 RevoScaleR 包来创建模型和转换数据。

+ [要开始使用 MicrosoftML](https://docs.microsoft.com/r-server/r/concept-what-is-the-microsoftml-package)

    了解有关快速、 可缩放的机器学习算法由 Microsoft research 开发的详细信息。
