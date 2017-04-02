---
title: "将 R 代码转换为在 R Services 中使用 | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "05/31/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "R"
ms.assetid: 0b11ab52-b2f9-4a4f-b1ab-68ba09c8adcc
caps.latest.revision: 12
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 11
---
# 将 R 代码转换为在 R Services 中使用
当将 R 代码从 R Studio 或另一个环境移到 SQL Server 中时，通常这些代码将正常工作无需进一步修改时添加到 *@script* 参数 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。 这是当您已开发您的解决方案使用 ScaleR 函数，使其相对简单，若要更改执行上下文尤其如此。    
    
但是，通常会想要修改 R 代码运行在 SQL Server 中，同时以利用具有更紧密的集成 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ，从而避免在昂贵的数据传输。   
   
   
## Resources  
  
若要查看如何在 SQL Server 中运行的 R 代码的示例，请参阅这些演练︰   
+ [SQL 开发人员的数据库中分析](../../advanced-analytics/r-services/in-database-advanced-analytics-for-sql-developers-tutorial.md)    
  演示如何使您的 R 代码更加模块化方法是将它放置在存储过程  
+ [端到端数据科学解决方案](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)    
  在 R 和 T-SQL 中包含特征工程的比较

## 对数据科学过程在 SQL Server 中的更改  
  
当您正处于 [!INCLUDE[rsql_rtvs_md](../../includes/rsql-rtvs-md.md)], ，RStudio，线程或其他环境中，典型的工作流即将到您的计算机中提取数据、 对数据进行分析以迭代方式，然后写出或显示的结果。 但是，在独立 R 代码迁移到 SQL Server 中，大部分此过程可以简化或委派给其他 SQL Server 工具︰

| 外部代码 | 在 SQL Server 中的 R |
|-------|-------|
| 引入数据| 输入的数据定义为数据库中的 SQL 查询 | 
| 汇总和实现数据可视化效果| 无更改;图形可以导出为图像或发送到远程计算机工作站|
|特征工程| 您可以使用 R 的数据库中，但可以会更有效地调用 T-SQL 函数或自定义 Udf|
|数据清理分析过程的一部分| 数据清理可以委派给 ETL 进程和提前执行|
|文件的输出预测| 输出预测，表或换行 `predict` 由应用程序的直接访问的存储过程中|
  

  
## 最佳实践  
  
+ 提前记下的依赖项，如所需的包。 在开发和测试环境中，则可能是可以安装程序包作为属于您的代码，但这是个糟糕的做法在生产环境中。 通知管理员，以便可以安装和部署代码之前测试包。  
+ 请键入问题的可能的数据的清单。 文档中的代码的每个部分的预期结果的架构。  
+ 标识如定型数据，还是与辅助源如因素、 其他分组变量等的预测的输入的数据的主数据源。 映射到的输入参数的最大数据集 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md)。  
+ 更改您输入的数据的语句来直接使用数据库。 而不是将数据移到本地的 CSV 文件，或进行重复 ODBC 调用，您将有更好的性能使用 SQL 查询或视图可以直接对数据库中，运行避免数据移动。  
+ 使用 SQL Server 查询计划，以确定可以并行执行的任务。 如果输入的查询可以实现并行化，设置 `@parallel=1` 到 sp_execute_external_script 您 arguments 的一部分。 并行处理使用此标志通常会随时 SQL Server 可以使用已分区表或分发在多个进程之间的查询和聚合结果结尾处。 
   并行处理使用此标志通常是不可能如果不使用需要要读取的所有数据的算法的定型模型，或者如果您需要创建聚合。 
+ 如有可能，替换与传统 R 函数 **ScaleR** 支持分布式的执行的函数。 有关详细信息，请参阅 [比较函数的小数位数 R 和 CRAN R 中](Summary%20of%20rx%20Functions.md)。
+ 查看您的 R 代码，以确定是否可以独立地执行或通过使用另一个存储的过程调用来更高效地执行的步骤。 例如，您可能决定分开进行功能工程或功能提取并在新列添加值。 使用 T-SQL 而不是基于数据集的计算的 R 代码。 Udf 和 R 功能工程任务的性能进行比较的 R 解决方案的一个示例，请参阅本教程︰ [数据科学的端到端演练](../../advanced-analytics/r-services/data-science-end-to-end-walkthrough.md)。  
  
    
## 限制    
 将 R 代码转换时，请记住下列限制︰    
   
**数据类型**    
-   支持所有的 R 数据类型。 但是， [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 支持更大的不同数据类型不是做到这一点 R、 发送时，将执行某些隐式数据类型转换 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据为 R，反之亦然。 您可能还需要显式强制转换或隐蔽的某些数据。    
    
- 支持 NULL 值。 R 使用 `na` 数据结构，以表示缺失值，这是类似于空值。    
    
- 有关详细信息，请参阅 [使用 R 数据类型](../../advanced-analytics/r-services/working-with-r-data-types.md)。    
 
 **输入和输出**   
+ 存储的过程参数的一部分，您可以定义只能有一个输入数据集。 此存储过程的输入的查询可以是任何有效的单个 SELECT 语句。 我们建议您对于最大数据集，使用此输入，并在需要时使用对 RODBC 调用获取较小数据集。 

+ 存储的过程执行前面的调用不能用作 sp_execute_external_script 的输入。    
    
+ 输入数据集中的所有列必须都映射到 R 脚本中的变量。 变量名称会自动映射。 例如，假设您的 R 脚本中包含的公式如下所示︰    
    
    ```    
    formula <- ArrDelay ~ CRSDepTime + DayOfWeek + CRSDepHour:DayOfWeek    
    ```    
    
     如果输入数据集不包含具有匹配名称 ArrDelay、 CRSDepTime、 DayOfWeek、 CRSDepHour 和星期的列，将引发错误。    

+ 您还可以作为输入提供多个标量参数。 但是，作为存储过程的参数中传递的任何变量 [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) 必须映射到 R 代码中的变量。 默认情况下，变量按名称进行映射。
+ 若要在 R 代码的输出中包含标量输入的变量，只是追加 **输出** 关键字时定义变量。             
+ 在 [!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)], ，R 代码最多可以将输出作为 data.frame 对象的单个数据集。 但是，您还可以输出多个标量值函数输出，以二进制格式，包括图形和 varbinary 格式中的模型。    
    
+ 通常可以输出而无需使用与 RESULT SETS UNDEFINED 选项指定输出列的名称由 R 脚本返回的数据集。 但是，在您想要输出的 R 脚本中的任何变量必须映射到 SQL 输出参数。
    
+ 如果 R 脚本使用参数 `@parallel=1`, ，必须定义输出架构。 原因是 SQL Server 以在结尾处收集的结果的同时，运行查询，可能会创建多个进程。 因此，可以创建并行进程之前，必须定义输出架构。

 **依赖关系**
 + 避免 R 代码从安装包。 在 SQL Server 上应事先安装包。  
  
  
  

