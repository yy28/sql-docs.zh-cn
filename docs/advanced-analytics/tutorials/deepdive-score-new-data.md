---
title: 使用 RevoScaleR 和 rxPredict-SQL Server 机器学习的新数据评分
description: 教程演练如何在 SQL Server 上使用 R 语言的数据进行评分。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: b96e70a6002722063a0be42c964c5e423503a0d7
ms.sourcegitcommit: 2827d19393c8060eafac18db3155a9bd230df423
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/27/2019
ms.locfileid: "58510344"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>为新数据 （SQL Server 和 RevoScaleR 教程） 评分
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程中属于[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

在此步骤中，您可以使用评分使用相同的自变量作为输入的另一个数据集在上一课中创建的逻辑回归模型。

> [!div class="checklist"]
> * 对新数据进行评分
> * 创建分数直方图

> [!NOTE]
> 有关其中某些步骤需要具有 DDL 管理员权限。

## <a name="generate-and-save-scores"></a>生成并保存分数
  
1. 更新 sqlScoreDS 数据源 (在中创建[第 2 课](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)) 若要使用在上一课中创建的列信息。
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. 若要确保不会丢失结果，请创建新的数据源对象。 然后，使用新的数据源对象来填充 RevoDeepDive 数据库中的新表。
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    此时尚未创建表。 此语句仅定义数据的容器。
     
3. 检查当前计算上下文中使用**rxGetComputeContext()**，并根据需要为服务器的设置计算上下文。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 作为预防措施，检查存在的输出表。 如果已存在具有相同的名称，则会出现错误，尝试写入新的表时。
  
    若要执行此操作，请调用函数 [rxSqlServerTableExists](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) 和 [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)，传递表名称作为输入。
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists**查询 ODBC 驱动程序，如果表存在，则返回 FALSE 否则，则返回 TRUE。
    + **rxSqlServerDropTable**执行 DDL，返回 TRUE，如果表已成功删除，FALSE 否则。

5. 执行[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)创建评分，并将其保存在数据源 sqlScoreDS 中定义的新表中。
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    rxPredict 函数是另一种函数，支持在远程计算上下文中运行。 可以使用**rxPredict**函数来从模型创建评分基于[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)， [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)，或者[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm)。
  
    - 参数 *writeModelVars* 在此处设置为 **TRUE** 。 这意味着新表中将包含用于估计的变量。
  
    - 参数 *predVarNames* 指定将在其中存储结果的变量。 此处传递一个新的变量`ccFraudLogitScore`。
  
    - rxPredict 的 type 参数定义计算预测的方式。 指定关键字**响应**生成分数的响应变量的规模。 或者，使用关键字**链接**生成分数基于基础链接函数，在这种情况下预测使用创建的逻辑刻度。

6. 不久，可以在 Management Studio 中刷新表的列表，以查看新的表及其数据。

7. 若要将其他变量添加到输出预测中，请使用 *extraVarsToWrite* 参数。  例如，在以下代码中，会将来自评分数据表的变量 custID 添加到预测的输出表中。
  
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

创建新表后，计算和显示 10,000 个预测评分的直方图。 如果指定下限和上限值，因此从数据库获取上述信息并将其添加到处理的数据，计算速度更快。

1. 创建新的数据源 sqlMinMax，查询数据库以获取下限和上限值。
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     从本示例中，可以看到使用 RxSqlServerData 数据源对象根据 SQL 查询、函数或存储过程定义任意数据集，然后将其用于 R 代码中非常容易。 变量不会存储实际值，只存储数据源定义；仅当在函数（如 rxImport）中使用此查询时，才会执行此查询以生成该值。
      
2. 调用[rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)函数可以跨计算上下文可共享的数据框中将的值。
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals <- as.vector(unlist(minMaxVals))
    ```

    **结果**
     
    ```R
    > minMaxVals
     
    [1] -23.970256   9.786345
    ```

3. 现在，最大和最小值均可用，使用值以创建另一个数据源生成评分。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. 数据源对象 sqlOutScoreDS 用于获得评分，并计算和显示直方图。 添加代码以根据需要设置计算上下文。
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **结果**
  
    ![R 创建的复杂直方图](media/rsql-sue-complex-histogram.png "R 创建的复杂直方图")
  
## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 R 转换数据](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)