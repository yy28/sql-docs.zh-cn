---
title: "使用 rxDataStep 执行区块分析（对数据科学的深入探讨）| Microsoft Docs"
ms.custom: 
ms.date: 10/03/2016
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
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: cc17b1365bc5938cb7e1c25e33ca42cafd2aa38e
ms.lasthandoff: 04/11/2017

---
# <a name="lesson-3-3---perform-chunking-analysis-using-rxdatastep"></a>课程 3-3 - 使用 rxDataStep 执行区块分析
rxDataStep 函数可用于在区块中处理数据，而不需要像在传统 R 中一样，将整个数据集加载到内存并对其进行一次性处理。其工作方式是在区块中读取数据并使用 R 函数依次处理每个区块的数据，然后将每个区块的摘要结果写入常见 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源。  
  
在本课程中，可使用 R 中的 *table* 函数来计算列联表。  
  
> [!TIP]  
> 本示例仅供教学使用。 如需将实际数据集制成表格，建议使用内置于 *RevoScaleR* 的 *rxCrossTabs* 或 **rxCube**函数，以上函数已针对此操作进行了优化。  
  
## <a name="partition-data-by-values"></a>按值的分区数据  
  
1.  首先，创建一个名为 *ProcessChunk* 的自定义 R 函数，该函数会对每个数据区块调用 *table* 函数。  
  
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
 
  
2.  设置服务器的计算上下文。  
  
    ```R  
    rxSetComputeContext( sqlCompute )   
    ```  
  
3.  定义 SQL Server 数据源以保存正在处理的数据。 首先将 SQL 查询分配给变量。   
  
    ```R  
    dayQuery <-  "SELECT DayOfWeek FROM AirDemoSmallTest"   
    ```  

4.  将该变量插入新 *数据源的* sqlQuery [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 参数。  
  
    ```R  
    inDataSource <- RxSqlServerData(sqlQuery = dayQuery,  
        connectionString = sqlConnString,    
        rowsPerRead = 50000,      
        colInfo = list(DayOfWeek = list(type = "factor",   
            levels = as.character(1:7))))    
    ```  
     如果在此数据源上运行 *rxGetVarInfo* ，你将会发现其仅包含单列： *Var 1: DayOfWeek，类型：因子，没有可用的因子级别*
     
5.  将此因子变量应用到源数据之前，先创建单独的表以保存中间结果。 同样，只需使用 *RxSqlServerData* 函数定义数据并删除同一名称的所有现有表。   
  
    ```R  
    iroDataSource = RxSqlServerData(table = "iroResults",   connectionString = sqlConnString)   
    # Check whether the table already exists.  
    if (rxSqlServerTableExists(table = "iroResults",  connectionString = sqlConnString))  { rxSqlServerDropTable( table = "iroResults", connectionString = sqlConnString) }   
    ```  
  
7.  现在调用自定义函数 *ProcessChunk* 函数，在读取数据的同时转换数据，方法是通过将其用作到 *rxDataStep* 函数的 *transformFunc* 参数。  
  
    ```R  
    rxDataStep( inData = inDataSource, outFile = iroDataSource, transformFunc = ProcessChunk, overwrite = TRUE)   
    ```  
  
8.  若要查看 *ProcessChunk*的中间结果，请将 *rxImport* 的结果分配到变量，然后将结果输出到控制台。  
  
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
  
10. 为了删除中间结果表，请另外调用  *rxSqlServerDropTable*。  
  
    ```R  
    rxSqlServerDropTable( table = "iroResults",     connectionString = sqlConnString)    
    ```  
  
## <a name="next-step"></a>下一步  
[第 4 课：在本地计算上下文中分析数据（对数据科学的深入探讨）](../../advanced-analytics/r-services/lesson-4-analyze-data-in-local-compute-context-data-science-deep-dive.md)  
  
## <a name="previous-step"></a>上一步  
[使用 rxDataStep 创建新的 SQL Server 表（对数据科学的深入探讨）](../../advanced-analytics/r-services/lesson-3-2-create-new-sql-server-table-using-rxdatastep.md)  
  
## <a name="see-also"></a>另请参阅  
[对数据科学的深入探讨：使用 RevoScaleR 包](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  


