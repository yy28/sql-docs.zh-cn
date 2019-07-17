---
title: 块区使用 rxDataStep 执行分析 RevoScaleR 的 SQL Server 机器学习
description: 有关如何分块的 SQL Server 上使用 R 语言的分布式分析数据的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 6ccc64c98f0519b33b6ba9da180c01e4478492f6
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962205"
---
# <a name="perform-chunking-analysis-using-rxdatastep-sql-server-and-revoscaler-tutorial"></a>块区使用 rxDataStep 执行分析 （SQL Server 和 RevoScaleR 教程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程中属于[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

在本课程中，您使用**rxDataStep**函数来处理数据的区块，而无需加载到内存中，如传统 R 中所示，一次处理整个数据集**RxDataStep**函数读取区块中的数据反过来，适用于每个数据区块的 R 函数，然后将每个区块的摘要结果保存到一个常见[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据源。 读取所有数据后，对结果进行组合。

> [!TIP]
> 通过使用本课程中，计算列联表**表**在 R 中的函数此示例适用于仅用于说明用途。 
> 
> 如果您需要实际的数据集制成表格，我们建议你使用**于**或**rxCube**中的函数**RevoScaleR**，针对进行了优化这种操作。

## <a name="partition-data-by-values"></a>按值的分区数据

1. 创建调用 R 的自定义 R 函数**表**函数对每个数据区块，并命名新函数**ProcessChunk**。
  
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
  
3. 定义要保存正在处理的数据的 SQL Server 数据源。 首先将 SQL 查询分配给变量。 然后，使用在该变量*sqlQuery*自变量的新的 SQL Server 数据源。
  
    ```R
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,
        connectionString = sqlConnString,
        rowsPerRead = 50000,
        colInfo = list(DayOfWeek = list(type = "factor",
            levels = as.character(1:7))))
    ```

4. （可选） 可以运行**rxGetVarInfo**对此数据源。 此时，它包含的单个列：*Var 1:DayOfWeek，类型： 因素，没有可用的因素级别*
     
5. 将此因子变量应用到源数据之前，先创建单独的表以保存中间结果。 同样，您只需使用**RxSqlServerData**函数来定义这些数据，并确定要删除具有相同名称的任何现有的表。
  
    ```R
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)
    # Check whether the table already exists.
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }
    ```
  
7.  调用自定义函数**ProcessChunk**来转换数据，它读取时，通过将其用作*transformFunc*参数**rxDataStep**函数。
  
    ```R
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)
    ```
  
8.  若要查看的中间结果**ProcessChunk**，将分配的结果**rxImport**给一个变量，然后将输出到控制台的结果。
  
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

10. 若要删除中间结果表，请调用**rxSqlServerDropTable**。
  
    ```R
    rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString)
    ```

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [SQL Server 的 R 教程](sql-server-r-tutorials.md)