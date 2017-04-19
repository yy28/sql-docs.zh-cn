---
title: "转换 R 代码以便在 R Services 中使用 | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 05/31/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
dev_langs:
- R
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 953fd7c7f5c3b8e968b682839c5144f8766fdb82
ms.lasthandoff: 04/11/2017

---
# <a name="converting-r-code-for-use-in-r-services"></a>转换 R 代码以便在 R Services 中使用
将 R 代码从 R Studio 或其他环境移到 SQL Server 时，在添加到 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 的 *@script* 参数后，该代码往往不需要经过进一步的修改即可正常工作。 如果解决方案是使用 ScaleR 函数（使更改执行上下文变得相对简单）开发的，则尤其如此。    
    
但是，通常我们想要修改 R 代码以便在 SQL Server 中运行，目的是利用与 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的更紧密集成，同时避免产生不菲的数据传输费用。   
   
   
## <a name="resources"></a>Resources  
  
若要查看有关如何在 SQL Server 中运行 R 代码的示例，请参阅以下演练：   
+ [In-Database Analytics for the SQL Developer](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)  （适用于 SQL 开发人员的数据库内分析）  
  演示如何通过将 R 代码包装在存储过程中，来提高 R 代码的模块化程度  
+ [End-to-End Data Science Solution](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)  （端到端数据科学解决方案）  
  在 R 和 T-SQL 中包含特征工程的比较

## <a name="changes-to-the-data-science-process-in-sql-server"></a>SQL Server 中数据科学过程的更改  
  
在 [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)]、RStudio 或其他环境中操作时，一个典型的工作流是将数据提取到计算机、以迭代方式分析数据，然后写出或显示结果。 但是，如果将独立的 R 代码迁移到了 SQL Server，则此过程的大部分步骤可以简化或委派给其他 SQL Server 工具：

| 外部代码 | SQL Server 中的 R |
|-------|-------|
| 引入数据| 将输入数据定义为数据库中的 SQL 查询 | 
| 汇总和可视化数据| 无变化；绘图可导出为图像或发送到远程工作站|
|特征工程| 可在数据库内使用 R，但调用 T-SQL 函数或自定义 UDF 可能更有效|
|分析过程的数据清理部分| 数据清理可以委派给 ETL 过程并提前执行|
|在文件中输出预测| 将预测输出到表中或者包装在 `predict` 存储过程中，供应用程序直接访问|
  

  
## <a name="best-practices"></a>最佳实践  
  
+ 提前记下依赖项，例如所需的包。 在开发和测试环境中，也许可以将包安装为代码的一部分，但在生产环境中，这是一种不好的做法。 通知管理员，以便在部署代码之前可以安装和测试包。  
+ 针对可能的数据类型问题创建一份查检表。 记录每个代码部分中预期结果的架构。  
+ 确定主要数据源（例如模型训练数据或用于预测的输入数据），以及辅助源（例如因子、附加分组变量，等等）。 将最大的数据集映射到 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 的输入参数。  
+ 更改输入数据语句，以便直接在数据库中操作。 不要将数据移到本地 CSV 文件或发出重复 ODBC 调用，而是使用可直接针对数据库运行的 SQL 查询或视图来避免数据移动，从而提高性能。  
+ 使用 SQL Server 查询计划来识别可以并行执行的任务。 如果输入查询可并行化，请将 `@parallel=1` 设置为 sp_execute_external_script 的参数的一部分。 只要 SQL Server 可以处理分区表或者在多个进程之间分布查询并最终聚合结果，就通常可以使用此标志进行并行处理。 
   如果用于训练模型的算法需要读取所有数据，或者你需要创建聚合，则通常无法使用此标志进行并行处理。 
+ 如有可能，请将传统的 R 函数替换为支持分布式执行的 **ScaleR** 函数。 有关详细信息，请参阅 [Comparison of Functions in Scale R and CRAN R](http://msdn.microsoft.com/library/8f8c91d7-50c3-4ca1-9427-a83d9d2ecd22)（Scale R 和 CRAN R 中函数的比较）。
+ 检查 R 代码，确定是否可以独立执行某些步骤，或者可以使用单独的存储过程调用来更有效地执行某些步骤。 例如，你可能会决定单独执行特征工程或特征提取，并在新列中添加值。 使用 T-SQL 而不是 R 代码进行基于集的计算。 有关对可用于特征工程任务的 UDF 和 R 性能进行比较的 R 解决方案的示例，请参阅以下教程：[Data Science End-to-End Walkthrough](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)（数据科学端到端演练）。  
  
    
## <a name="restrictions"></a>限制    
 转换 R 代码时，请记住以下限制：    
   
**数据类型**    
-   支持所有 R 数据类型。 但是，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持的数据类型比 R 更广泛，因此，在将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据发送到 R 时，将执行某些隐式数据类型转换，反之亦然。 可能还需要显式强制转换或转换某些数据。    
    
- 支持 NULL 值。 R 使用 `na` 数据构造来表示缺失值（类似于 null 值）。    
    
- 有关详细信息，请参阅 [使用 R 数据类型](../../advanced-analytics/r-services/working-with-r-data-types.md)。    
 
 **Inputs and outputs**   
+ 只能将一个输入数据集定义为存储过程参数的一部分。 存储过程的此输入查询可以是任一有效的单个 SELECT 语句。 对于最大的数据集，我们建议使用此输入，并根据需要使用 RODBC 调用获取较小的数据集。 

+ 前面带有 EXECUTE 的存储过程调用不能用作 sp_execute_external_script 的输入。    
    
+ 输入数据集中的所有列必须映射到 R 脚本中的变量。 变量自动按名称映射。 例如，假设 R 脚本包含如下所示的公式：    
    
    ```    
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek    
    ```    
    
     如果输入数据集不包含具有匹配名称 ArrDelay、CRSDepTime、DayOfWeek、CRSDepHour 和 DayOfWeek 的列，将引发错误。    

+ 也可以提供多个标量参数作为输入。 但是，作为 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 存储过程的参数传入的任何变量必须映射到 R 代码中的变量。 默认情况下，变量按名称映射。
+ 若要在 R 代码的输出中包含标量输入变量，只需在定义变量时追加 **OUTPUT** 关键字。             
+ 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中，R 代码限制为输出单个数据集作为 data.frame 对象。 但是，你也可以输出多个标量输出，包括采用 binary 格式的绘图，以及采用 varbinary 格式的模型。    
    
+ 通常，可以使用 WITH RESULT SETS UNDEFINED 输出 R 脚本返回的数据集，而无需指定输出列的名称。 但是，要输出的 R 脚本中的任何变量必须映射到 SQL 输出参数。
    
+ 如果 R 脚本使用参数 `@parallel=1`，则必须定义输出架构。 原因是 SQL Server 可能会创建多个进程来并行运行查询，最后收集结果。 因此，必须先定义输出架构，然后才能创建并行进程。

 **依赖关系**
 + 避免从 R 代码安装包。 在 SQL Server 上，应该提前安装包，并且必须使用 R Services 所用的默认包库。  
  
  
  



