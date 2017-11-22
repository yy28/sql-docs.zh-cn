---
title: "新数据评分 |Microsoft 文档"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 87056467-f67f-4d72-a83c-ac052736d85d
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 752f4722906d580c7b1da208ac9bd641d0bae1c5
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="score-new-data"></a>对新数据进行评分

现在，你拥有一个可用于预测的模型，并将为它提供来自 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的数据，以便生成某些预测。

你将使用逻辑回归模型 logitObj 为使用与输入相同的独立变量的其他数据集创建评分。

> [!NOTE]
> 其中一些步骤需要具有 DDL 管理员权限。

## <a name="generate-and-save-scores"></a>生成并保存评分
  
1. 更新之前设置的数据源 sqlScoreDS，以添加所需的列信息。
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. 为了确保不会丢失结果，请创建新的数据源对象，并将其填充到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据库的新表中。
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
     此时尚未创建表。 此语句仅定义数据的容器。
     
3. 检查当前计算上下文，并将计算上下文设置为服务器（如果需要）。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 在运行生成结果的预测函数前，需要检查是否存在现有输出表。 否则，当你尝试写入新的表时将收到错误。
  
    若要执行此操作，请调用函数 rxSqlServerTableExists 和 rxSqlServerDropTable，传递表名称作为输入。
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    -  函数 rxSqlServerTableExists 查询的 ODBC 驱动程序，如果该表存在，则返回 FALSE 否则，则返回 TRUE。
    -  函数 rxSqlServerDropTable 函数执行 DDL，如果表已成功删除，则返回 FALSE 否则，则返回 TRUE。
  
5. 现在，你可以使用 rxPredict 函数来创建评分，并将其保存到在数据源 sqlScoreDS 中定义的新表中。
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    RxPredict 函数是支持远程计算上下文中运行的另一个函数。 RxPredict 函数可用于从创建使用 rxLinMod、 rxLogit 或 rxGlm 的模型创建评分。
  
    - 参数 *writeModelVars* 在此处设置为 **TRUE** 。 这意味着新表中将包含用于估计的变量。
  
    - 参数 *predVarNames* 指定将在其中存储结果的变量。 此处传递一个新变量 ccFraudLogitScore。
  
    - *类型*rxPredict 参数定义你希望如何计算预测。 指定关键字 **response** 以基于应变量的刻度生成评分，或使用关键字 **link** 以基于基础链接函数生成评分，在这种情况下，预测将位于逻辑刻度上。

6. 不久，可以在 Management Studio 中刷新表的列表，以查看新的表及其数据。

7. 若要将其他变量添加到输出预测中，可以使用 extraVarsToWrite 参数。  例如，在以下代码中，会将来自评分数据表的变量 custID 添加到预测的输出表中。
  
    ```R
    rxPredict(modelObject = logitObj,
            data = sqlScoreDS,
            outData = sqlServerOutDS,
            predVarNames = "ccFraudLogitScore",
              type = "link",
            writeModelVars = TRUE,
            extraVarsToWrite = "custID",
            overwrite = TRUE)
    ```

## <a name="display-scores-in-a-histogram"></a>显示直方图中的评分

创建新表后，将计算并显示具有 10,000 个预测评分的直方图。 如果指定下限值和上限值，计算速度会更快，可从数据库获得这些值将并它们添加到需要处理的数据中。

1. 创建新数据源 sqlMinMax，查询数据库以获取下限值和上限值。
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     在此示例中，你可以了解如何轻松使用 RxSqlServerData 数据源对象来定义基于 SQL 的查询、 函数或存储的过程的任意数据集，然后使用 R 代码中的那些。 该变量不会存储的实际值，只需数据源定义;执行该查询以仅当使用中所示 rxImport 的函数时生成的值。
      
2. 调用 rxImport 函数可以跨计算上下文中可以共享的数据帧将的值。
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals \<- as.vector(unlist(minMaxVals))
  
    ```
     **结果**
     
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3. 现在，可最大和最小值，使用的值创建评分的数据源。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. 最后，使用评分数据源对象来获取评分的数据，并计算和显示一个直方图。 添加代码以根据需要设置计算上下文。
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **结果**
  
    ![R 创建的复杂直方图](media/rsql-sue-complex-histogram.png "R 创建的复杂直方图")
  
## <a name="next-step"></a>下一步

[转换数据使用 R](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

## <a name="previous-step"></a>上一步

[创建模型](../../advanced-analytics/tutorials/deepdive-create-models.md)


