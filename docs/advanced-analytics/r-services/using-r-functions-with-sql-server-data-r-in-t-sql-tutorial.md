---
title: "对 SQL Server 数据使用 R 函数（T-SQL 中的 R 教程）| Microsoft Docs"
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
ms.assetid: e2fe5d90-eee9-4daf-9eae-21d17b3ef320
caps.latest.revision: 8
author: jeannt
ms.author: jeannt
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: ad248eda31c21234944cf6f7a7c65ca963625c45
ms.lasthandoff: 04/11/2017

---
# <a name="using-r-functions-with-sql-server-data-r-in-t-sql-tutorial"></a>对 SQL Server 数据使用 R 函数（T-SQL 中的 R 教程）
现在，你已熟悉了基本操作，是时候使用 R 做一些有趣的事情了。例如，许多高级统计功能可能比较复杂，难以使用 T-SQL 来实现，但可能只需要一行 R 代码便可实现。  使用 R Services，可以轻松在存储过程中嵌入 R 实用工具脚本。  
 
在这些示例中，你将在 SQL Server 存储过程中嵌入 R 数学函数和实用工具函数。

## <a name="create-a-stored-procedure-to-generate-random-numbers"></a>创建一个存储过程来生成随机数字  
  
为简单起见，我们将使用 R `stats` 包，该包默认情况下随 R Services 安装并加载。 此包中包含数百个用于执行常用统计任务的函数，其中，`rnorm` 函数在给定了标准差和平均数的情况下使用正态分布生成指定数量的随机数字。    

例如，以下 R 代码在给定了标准差 3 的情况下返回平均数为 50 的 100 个数字。 

```R
as.data.frame(rnorm(100, mean = 50, sd = 3));
```

要从 T-SQL 调用此行 R 代码，请运行 sp_execute_external_script 并在 R 脚本参数中添加此 R 函数，如下所示： 
   
```sql    
EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N' 
         OutputDataSet <- as.data.frame(rnorm(100, mean = 50, sd =3));'    
    , @input_data_1 = N'   ;'    
      WITH RESULT SETS (([Density] float NOT NULL));    
```    

如果你希望更轻松地生成不同的一组随机数字，那该怎么办？ 

这很简单：定义一个从用户那里获取参数的存储过程。 然后，将那些参数作为变量传递给 R 脚本。 

```sql
CREATE PROCEDURE MyRNorm (@param1 int, @param2 int, @param3 int)
AS
    EXEC sp_execute_external_script    
      @language = N'R'    
    , @script = N'
         OutputDataSet <- as.data.frame(rnorm(mynumbers, mymean, mysd));'    
    , @input_data_1 = N'   ;' 
    , @params = N' @mynumbers int, @mymean int, @mysd int'  
    , @mynumbers = @param1
    , @mymean = @param2
    , @mysd = @param3
    WITH RESULT SETS (([Density] float NOT NULL));   
```
+ 第一行定义了在执行该存储过程时必需的每个 SQL 输入参数。 
+ 以 `@params` 开头的行定义了 R 代码使用的所有变量，以及对应的 SQL 数据类型。 
+ 紧跟在后面的行将 SQL 参数名称映射到对应的 R 变量名称。

现在，你已将 R 函数包装在了一个存储过程中，你可以轻松调用该函数并传入不同的值，如下所示：

```sql
EXEC MyRNorm @param1 = 100,@param2 = 50, @param3 = 3
```  

**说明**

+ 想要安装更多 R 包以获得更高级的统计功能？ 请参阅[安装和管理 R 包](../../advanced-analytics/r-services/installing-and-managing-r-packages.md)。 
+ R Services 团队创建了一个 R 包来帮助你将独立的 R 代码转换为可以轻松使用 SQL Server 存储过程进行参数化的格式。 有关详细信息，请参阅[如何使用 sqlrutils 创建存储过程](../../advanced-analytics/r-services/how-to-create-a-stored-procedure-using-sqlrutils.md)。 
    
## <a name="use-r-utility-functions-for-troubleshooting"></a>使用 R 实用工具函数进行故障排除 
  
默认情况下，R Services 包括了 `utils` 包，该包提供了用于调查当前 R 环境的各种实用工具函数。 如果你发现你的 R 代码在 SQL Server 中执行时和在环境外执行时执行方式存在差异，则上述函数会比较有用。

例如，你可以使用 R `memory.limit()` 函数获取当前 R 环境的内存。 因为 `utils` 包默认情况下已安装但未加载，因此你必须首先使用 `library()` 函数加载该包。    
    
```sql    
EXECUTE sp_execute_external_script    
      @language = N'R'    
    , @script = N'    
        library(utils);    
        mymemory <- memory.limit();    
        OutputDataSet <- as.data.frame(mymemory);'    
    , @input_data_1 = N' ;'    
WITH RESULT SETS (([Col1] int not null));    
```    

还可以使用 R 中的系统计时函数（例如 `system.time` 和 `proc.time`）来捕获 R 进程使用的时间并分析性能问题。 

有关示例，请参阅以下教程：[创建数据功能](https://msdn.microsoft.com/library/mt634286.aspx)。 在此演练中，在解决方案中嵌入了 R 计时函数，它们用来对基于数据创建功能的以下两种方法的性能进行比较：R 函数与 T-SQL 函数。 


## <a name="next-step"></a>下一步

接下来，你将在 SQL Server 中使用 R 创建一个预测模型。

[创建预测模型](../../advanced-analytics/r-services/create-a-predictive-model-r-in-t-sql-tutorial.md)

    
    



