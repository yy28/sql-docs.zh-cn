---
title: "通过模型预测和绘图（T-SQL 中的 R 教程）| Microsoft Docs"
ms.custom: 
ms.date: 03/10/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
- SQL
ms.assetid: 46babd8a-a331-44fc-bbd6-24daf58865e1
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 2d106064e4b3b6d71d734785e6fb3bf3b3b7226d
ms.lasthandoff: 04/11/2017

---
# <a name="predict-and-plot-from-model-r-in-t-sql-tutorial"></a>通过模型预测和绘图（T-SQL 中的 R 教程）
若要为新数据评分，需要从表中获取一个已训练的模型，然后调用用作预测基础的一组新数据。


## <a name="create-the-table-of-new-speeds"></a>创建新速度表 

你是否注意到，原始训练数据在每小时 25 英里的速度处就不再继续了？ 这是因为原始数据基于 1920 年的试验！ 

你可能想要知道，假设 20 世纪 20 年代的汽车能够跑到 60 甚至 100 mph，那么停止下来需要花费多长时间？ 若要回答此问题，需要提供一些新的速度值。

```sql
CREATE TABLE [dbo].[NewCarSpeed]([speed] [int] NOT NULL,
    [distance] [int]  NULL) ON [PRIMARY]
GO
INSERT [dbo].[NewCarSpeed] (speed)
VALUES (40),  (50),  (60), (70), (80), (90), (100)
```

## <a name="predict-stopping-distance"></a>预测停止距离


目前，表中可能包含多个 R 模型，其中的所有模型都是使用不同的参数或算法构建的，或者已根据不同的数据子集进行训练。  

![rsql_basictut_listofmodels](../../advanced-analytics/r-services/media/rsql-basictut-listofmodels.png)

若要基于特定的模型获取预测，必须编写执行以下操作的 SQL 脚本：

1. 获取所需的模型
2. 获取新的输入数据
3. 调用与该模型兼容的 R 预测函数

在此示例中，由于模型基于 **RevoScaleR** 包随附的 **rxLinMod** 算法，因此你应该调用 `rxPredict` 函数，而不是泛型 R `predict` 函数。

```sql
DECLARE @speedmodel varbinary(max) = (SELECT model FROM [dbo].[stopping_distance_models] WHERE model_name = 'default model');
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
**说明**

+ 使用 SELECT 语句从表中获取单个模型，并将它作为输入参数传递。
+  从表中检索模型后，针对该模型调用 `unserialize` 函数。
+  将带有相应参数的 `rxPredict` 函数应用到该模型，并提供新的输入数据。
+ 我们在测试时使用了 `str` 函数来检查从 R 返回的数据的架构。以后始终可以删除该语句。
+ 可将列名添加到 R 脚本中包含的输出数据框架，但这里我们只是使用了WITH RESULTS 子句。
+ 若要从原始数据集中连同预测结果一起返回列，请将源列与预测值列串联为 R 脚本的一部分，然后将数据框架返回到 SQL Server。 

**结果**

![rsql_basictut_scoringresults_smalldata](../../advanced-analytics/r-services/media/rsql-basictut-scoringresults-smalldata.PNG)



## <a name="perform-scoring-in-parallel"></a>并行执行评分

对于这个微小的数据集，很快就返回了预测结果。 但是，如何快速做出大量预测？ 在 SQL Server 中，有多种方法可以加快操作，尤其是操作可并行化时。 具体而言，对于评分，一种简单的方式是将 *@parallel* 参数添加到 `sp_execute_external_script`，并将值设置为 **1**。 

假设你已获取一个大得多的可能车速表，其中包含几十万个值。 社区提供的许多示例 T-SQL 脚本可帮助你生成数据表，本文不会重新生成这些表。 假设某个列包含多个整数，你想要使用该列作为模型中 `speed` 的输入。

为此，只需运行相同的预测查询，但要替换为更大的数据集，并添加 _@parallel = 1_ 参数。

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

**说明**


+ 仅当使用极大型数据时，并行执行才能提供优势。 此外，获取数据的 SQL 查询必须能够生成并行查询计划。

+ 使用并行执行的选项时，**必须**提前使用 WITH RESULT SETS 子句指定输出结果架构。 提前指定输出架构可睛 SQL Server 聚合多个并行数据集，否则可能会生成未知的架构。    
    

请注意，如果你是在*培训*模型而不是*评分*，此参数通常不会产生影响。 根据模型类型，创建模型过程可能需要在读取所有行之后才能创建摘要。 

  因此，若要在训练模型时获得并行处理的好处，我们建议使用 **ScaleR** 算法之一。 这些算法旨在自动分散处理，即使未在 sp_execute_external_script 调用中指定 *@parallel = 1*。 有关如何使用 ScaleR 实现最佳性能的指导，请参阅 [ScaleR Distributed Computing](https://msdn.microsoft.com/microsoft-r/scaler-distributed-computing)（ScaleR 分布式计算）。
    
## <a name="create-an-r-plot-of-the-model"></a>创建模型的 R 绘图

许多客户端（包括 SQL Server Management Studio）无法直接显示使用 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 创建的绘图。 在 R Services 中生成 R 绘图的一般过程是将绘图创建为 R 代码的一部分，然后将图像写入某个文件。 

或者，可将序列化的二进制绘图对象返回到可以显示图像的应用程序，例如 Reporting Services。

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

**说明**

+ `tempfile` 函数将返回一个可用作文件名的字符串，但该文件实际上尚未生成。 
+ 对于 `tempfile` 的参数，可以指定前缀和文件扩展名，以及 tmpdir。 为了验证文件名和路径，我们使用 `str()` 列显了一条消息。
+ `jpeg` 函数使用指定的参数创建 R 设备。
+ 创建绘图后，可在其中添加更多的视觉特征。 在本例中，已使用 `abline` 添加回归线。
+ 添加完绘图特征后，必须使用 `dev.off()` 函数关闭图形设备。
+ `readBin` 函数使用要读取的文件、格式规范以及记录数。 **rb** 关键字表示该文件是二进制文件，而不包含文本。

**结果**

![rsql_basictut_plotresult_small](../../advanced-analytics/r-services/media/rsql-basictut-plotresult-small.png)

如果想要使用 R 的某些强大图形包创建更复杂的绘图，我们建议阅读以下文章。 在这两篇文章中，都需要使用流行的 **ggplot2** 包。

+ [Loan Classification using SQL Server 2016 R Services](https://blogs.msdn.microsoft.com/microsoftrservertigerteam/2016/09/27/loan-classification-using-sql-server-2016-r-services/)（使用 SQL Server 2016 R Services 进行借贷分类）基于保险数据的端到端方案。 此外，还需要 **reshape** 包。
+ [Create Graphs and Plots Using R](https://msdn.microsoft.com/library/mt629162.aspx)（使用 R 创建图形和绘图）：基于纽约市出租车数据的端到端解决方案第 2 课。


## <a name="conclusion"></a>结语

将 R 与 SQL Server 集成后，可以更方便地大规模部署 R 解决方案，利用 R 和关系数据库的最佳功能实现高性能数据处理和快速 R 分析。 

若要继续学习结合使用 R 和 SQL Server 的解决方案，请参阅 Microsoft 数据科学和 R Services 开发团队创建的教程与端到端方案： 

+  [SQL Server R Services 教程](../../advanced-analytics/r-services/sql-server-r-services-tutorials.md)

有关使用新 RevoScaleR 包的指导，请参阅有关 [Microsoft R](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started) 的以下资源：

+ [Explore R and ScaleR in 25 functions](https://msdn.microsoft.com/microsoft-r/microsoft-r-getting-started-tutorial)（通过 25 个函数探索 R 和 ScaleR）
+ [Fitting Linear Models](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-linear-model)（拟合线性模型）
+ [Models in RevoScaleR](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-models)（RevoScaleR 中的模型）
    
    
    






