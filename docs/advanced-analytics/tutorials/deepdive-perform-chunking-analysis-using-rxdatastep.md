---
title: "块区使用执行分析 rxDataStep （SQL 和 R 深入） |Microsoft 文档"
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 4290ee5f-be90-446a-91e8-3095d694bd82
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 7e47db93c014f2512f40afc88d9e9fb0f2031976
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-and-r-deep-dive"></a>块区使用执行分析 rxDataStep （SQL 和 R 深入）

本文是有关如何使用数据科学深入了解教程的一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

在本课程中，你使用**rxDataStep**函数来处理数据的区块，而无需整个数据集被加载到内存并处理一次如下所示传统。**RxDataStep**函数读取区块中的数据反过来，适用于每个数据块区的 R 函数，然后将每个区块的摘要结果保存到一个常见[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据源。 读取所有数据后，对结果进行组合。

> [!TIP]
> 通过使用本课程中，为计算应急表`table`函数中。本示例旨在仅供指导。 
> 
> 如果你需要制成表格实际数据集，我们建议你使用**rxCrossTabs**或**rxCube**中函数**RevoScaleR**，针对进行了优化这有点操作。

## <a name="partition-data-by-values"></a>值的分区数据

1. 创建自定义 R 调用的函数，R`table`函数对每个区块的数据，并命名新函数`ProcessChunk`。
  
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
  
3. 定义 SQL Server 数据源以容纳要处理的数据。 首先将 SQL 查询分配给变量。 然后，使用该变量在*sqlQuery*的一个新的自变量[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据源。
  
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```
4. （可选） 你可以运行**rxGetVarInfo**对此数据源。 此时，它包含单个列： *Var 1: DayOfWeek，键入： 不因数，可用任何因素级别*
     
5. 将此因子变量应用到源数据之前，先创建单独的表以保存中间结果。 同样，您只需使用 RxSqlServerData 函数来定义的数据，使确实要删除具有相同名称的任何现有表。
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  调用自定义函数`ProcessChunk`来转换数据，它读取时，通过使用其作为*transformFunc*参数**rxDataStep**函数。
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  若要查看的中间结果`ProcessChunk`，分配的结果**rxImport**给一个变量，然后输出到控制台的结果。
  
    ```R
    iroResults <- rxImport(iroDataSource)
    iroResults
    ```

**部分结果**

|      |    @shouldalert  |   2   |  3   |  4   |  5  |   6   |  7 |
| --- | ---  | --- | ---  |  ---  | ---  | ---  | --- |
| @shouldalert | 8228 | 8924 | 6916 | 6932 | 6944 | 5602 | 6454 |
| 2  | 8321  | 5351 | 7329 | 7411 | 7409 | 6487 | 7692 |

9. 若要计算所有区块的最终结果，可以汇总各列，并将结果显示在控制台中。

    ```R
    finalResults <- colSums(iroResults)
    finalResults
    ```

 **结果**
  @shouldalert  |   2  |   3  |   4  |   5  |   6  |   7
---  |   ---  |   ---  |   ---  |   ---  |   ---  |   ---
97975 | 77725 | 78875 | 81304 | 82987 | 86159 | 94975 

10. 要移除的中间结果表，请先调用**rxSqlServerDropTable**。
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-step"></a>下一步

[在本地计算上下文中分析数据](../../advanced-analytics/tutorials/deepdive-analyze-data-in-local-compute-context.md)

## <a name="previous-step"></a>上一步

[使用 rxDataStep 创建新的 SQL Server 表](../../advanced-analytics/tutorials/deepdive-create-new-sql-server-table-using-rxdatastep.md)
