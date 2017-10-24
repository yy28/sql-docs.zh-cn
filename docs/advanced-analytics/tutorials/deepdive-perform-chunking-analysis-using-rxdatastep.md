---
title: "分块使用执行分析 rxDataStep |Microsoft 文档"
ms.custom: 
ms.date: 05/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
dev_langs:
- R
ms.assetid: 4290ee5f-be90-446a-91e8-3095d694bd82
caps.latest.revision: 17
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: af375ddf99794b748699355203becd137227fbcd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="perform-chunking-analysis-using-rxdatastep"></a>使用 rxDataStep 执行区块分析

rxDataStep 函数可用于在区块中处理数据，而不需要像在传统 R 中一样，将整个数据集加载到内存并对其进行一次性处理。其工作方式是在区块中读取数据并使用 R 函数依次处理每个区块的数据，然后将每个区块的摘要结果写入常见 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源。

在本课程中，您将通过使用练习此技术`table`R，来计算应急表中的函数。

> [!TIP]
> 本示例仅供教学使用。 如果你需要制成表格实际数据集，我们建议你使用**rxCrossTabs**或**rxCube**中函数**RevoScaleR**，针对进行了优化这有点操作。

## <a name="partition-data-by-values"></a>按值的分区数据

1. 首先，创建自定义 R 调用的函数，*表*函数对每个区块的数据，并将其命名`ProcessChunk`。
  
    ```R
    ProcessChunk <- function( dataList) {
    # Convert the input list to a data frame and compute contingency table
    chunkTable <- table(as.data.frame(dataList))
  
    # Convert table output to a data frame with a single row
    varNames <- names(chunkTable)
    varValues <- as.vector(chunkTable)
    dim(varValues) <- c(1, length(varNames))
    chunkDF <- as.data.frame(varValues)
    names(chunkDF) <- varNames
  
    # Return the data frame, which has a single row
    return( chunkDF )
    }
    ```

2. 设置服务器的计算上下文。
  
    ```R
    rxSetComputeContext( sqlCompute )
    ```
  
3. 定义 SQL Server 数据源以保存正在处理的数据。 首先将 SQL 查询分配给变量。
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    ```

4. 将该变量插入新 *数据源的* sqlQuery [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 参数。
  
    ```R
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```
     如果在此数据源上运行 *rxGetVarInfo* ，你将会发现其仅包含单列： *Var 1: DayOfWeek，类型：因子，没有可用的因子级别*
     
5. 将此因子变量应用到源数据之前，先创建单独的表以保存中间结果。 同样，你只需使用 RxSqlServerData 函数来定义数据，并删除具有相同名称的任何现有表。
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  现在你将调用自定义函数`ProcessChunk`来转换数据，它读取时，通过使用其作为*transformFunc* rxDataStep 函数参数。
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  若要查看的中间结果`ProcessChunk`将 rxImport 的结果赋给变量，然后将结果输出到控制台。
  
    ```R
    iroResults <- rxImport(iroDataSource)
    iroResults
    ```

**部分结果**

|      |    1  |   2   |  3   |  4   |  5  |   6   |  7 |
| --- | ---  | --- | ---  |  ---  | ---  | ---  | --- |
| 1 | 8228 | 8924 | 6916 | 6932 | 6944 | 5602 | 6454 |
| 2  | 8321  | 5351 | 7329 | 7411 | 7409 | 6487 | 7692 |

9. 若要计算所有区块的最终结果，可以汇总各列，并将结果显示在控制台中。

    ```R
    finalResults <- colSums(iroResults)
    finalResults
    ```

 **结果**
  1  |   2  |   3  |   4  |   5  |   6  |   7
---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---
97975 | 77725 | 78875 | 81304 | 82987 | 86159 | 94975 

10. 若要删除的中间结果表，请对 rxSqlServerDropTable 另一个调用。
  
    ```R
    rxSqlServerDropTable( table = "iroResults",     connectionString = sqlConnString)
    ```

## <a name="next-step"></a>下一步

[分析本地计算上下文; 中的数据](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)

## <a name="previous-step"></a>上一步

[创建新的 SQL Server 表使用 rxDataStep](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)



