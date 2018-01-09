---
title: "新数据 （SQL 和 R 深入） 评分 |Microsoft 文档"
ms.custom: 
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 87056467-f67f-4d72-a83c-ac052736d85d
caps.latest.revision: "17"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 9b4192252edff42275acff6902677e3dadd3122e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="score-new-data-sql-and-r-deep-dive"></a>新数据 （SQL 和 R 深入） 评分

本文是有关如何使用数据科学深入了解教程的一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

在此步骤中，你可以使用逻辑回归模型，你更早版本，创建用于创建使用相同的自变量作为输入的另一个数据集评分。

> [!NOTE]
> 这些步骤的某些需要 DDL 管理员权限。

## <a name="generate-and-save-scores"></a>生成并保存评分
  
1. 更新数据源时更早版本，设置了`sqlScoreDS`、 添加所需的列信息。
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. 若要确保不会丢失结果，请创建一个新的数据源对象。 然后，使用新的数据源对象来填充的新表中[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。
  
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
  
    -  函数 rxSqlServerTableExists 会查询 ODBC 驱动程序，如果表存在，则返回 TRUE，否则返回 FALSE。
    -  该函数**rxSqlServerDropTable**执行 DDL 并返回 TRUE，如果表已成功删除，则 FALSE 否则。
    - 引用为这两个函数可在此处找到： [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)
  
5. 现在你已准备好使用[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)函数来创建评分，并将它们保存在数据源中定义的新表`sqlScoreDS`。
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    rxPredict 函数是另一种函数，支持在远程计算上下文中运行。 可以使用 **rxPredict** 函数从使用 [rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)、[rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit) 或 [rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm) 创建的模型创建评分。
  
    - 参数 *writeModelVars* 在此处设置为 **TRUE** 。 这意味着新表中将包含用于估计的变量。
  
    - 参数 *predVarNames* 指定将在其中存储结果的变量。 此处将传递一个新变量， `ccFraudLogitScore`。
  
    - rxPredict 的 type 参数定义计算预测的方式。 指定关键字**响应**生成分数根据响应变量的规模。 或者，使用关键字**链接**以生成基于对基础链接函数，在这种情况下的评分预测使用创建的逻辑扩展。

6. 不久，可以在 Management Studio 中刷新表的列表，以查看新的表及其数据。

7. 若要将其他变量添加到输出预测中，请使用 *extraVarsToWrite* 参数。  例如，在下面的代码中，变量`custID`从评分的数据表添加到输出表的预测。
  
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

## <a name="display-scores-in-a-histogram"></a>在直方图中显示分数

创建新的表后，可以计算并显示 10,000 的预测评分的直方图。 如果你指定的下限和上限值，因此获取那些项目从数据库并且将它们添加到你的工作数据，计算速度更快。

1. 创建新的数据源， `sqlMinMax`，查询数据库以获取下限和上限值。
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     从本示例中，可以看到使用 RxSqlServerData 数据源对象根据 SQL 查询、函数或存储过程定义任意数据集，然后将其用于 R 代码中非常容易。 变量不会存储实际值，只存储数据源定义；仅当在函数（如 rxImport）中使用此查询时，才会执行此查询以生成该值。
      
2. 调用[rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)函数可以跨计算上下文中可以共享的数据帧将的值。
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals \<- as.vector(unlist(minMaxVals))
  
    ```
     **结果**
     
     *> minMaxVals*
     
     *[1] -23.970256   9.786345*
  
3. 现在，可最大和最小值，使用的值创建另一个数据源生成评分。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. 使用数据源对象`sqlOutScoreDS`获取评分，并计算和显示直方图。 添加代码以根据需要设置计算上下文。
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **结果**
  
    ![R 创建的复杂直方图](media/rsql-sue-complex-histogram.png "R 创建的复杂直方图")
  
## <a name="next-step"></a>下一步

[使用 R 转换数据](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)

## <a name="previous-step"></a>上一步

[创建模型](../../advanced-analytics/tutorials/deepdive-create-models.md)


