---
title: 使用 RevoScaleR rxDataStep 执行区块分析
description: 本教程演示如何使用 R 语言在 SQL Server 上对数据进行分块。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
monikerRange: '>=sql-server-2016||>=sql-server-linux-ver15||=sqlallproducts-allversions'
ms.openlocfilehash: ed22020b162bfac9f35eb8328ea6409903191a4c
ms.sourcegitcommit: 321497065ecd7ecde9bff378464db8da426e9e14
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/01/2019
ms.locfileid: "68714897"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>使用 rxDataStep 执行区块分析 (SQL Server 和 RevoScaleR 教程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本课程是有关如何在 SQL Server 中使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)的[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的一部分。

在本课中, 您将使用**rxDataStep**函数来处理块区中的数据, 而不需要将整个数据集加载到内存中并一次进行处理, 就像在传统的 R 中一样。**RxDataStep**函数读取区块中的数据, 依次对每个数据块应用 R 函数, 然后将每个区块的摘要结果保存到公共[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据源。 读取所有数据后, 结果将合并。

> [!TIP]
> 在本课中, 您将通过使用 R 中的**表**函数来计算应急表。此示例仅用于说明目的。 
> 
> 如果需要制表现实数据集, 建议使用**RevoScaleR**中的**rxCrossTabs**或**rxCube**函数, 这些函数针对此类操作进行了优化。

## <a name="partition-data-by-values"></a>按值对数据进行分区

1. 创建一个自定义 R 函数, 该函数对每个数据块调用 R**表**函数, 并将新函数命名为**ProcessChunk**。
  
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
    rxSetComputeContext(sqlCompute)
    ```
  
3. 定义用于保存正在处理的数据的 SQL Server 数据源。 首先将 SQL 查询分配给变量。 然后, 在新 SQL Server 数据源的*sqlQuery*参数中使用该变量。
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. 或者, 您可以在此数据源上运行**rxGetVarInfo** 。 此时, 它包含单个列:*Var 1:DayOfWeek, 类型: 因素, 没有可用的因素级别*
     
5. 将此因子变量应用到源数据之前，先创建单独的表以保存中间结果。 同样, 只需使用**RxSqlServerData**函数来定义数据, 并确保删除任何同名的现有表。
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  调用自定义函数**ProcessChunk** , 以在读取数据时对其进行转换, 方法是将其用作**RxDataStep**函数的*transformFunc*参数。
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  若要查看**ProcessChunk**的中间结果, 请将**rxImport**的结果分配给一个变量, 然后将结果输出到控制台。
  
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

10. 若要删除中间结果表, 请调用**rxSqlServerDropTable**。
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [SQL Server 的 R 教程](sql-server-r-tutorials.md)