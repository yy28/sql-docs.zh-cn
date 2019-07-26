---
title: 使用 RevoScaleR 和 rxPredict 对新数据进行评分
description: 有关如何使用 R 语言对数据进行评分的教程演练 SQL Server。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 8d38f2183078ee87fdb53e6333ecd13e85f3c65e
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469664"
---
# <a name="score-new-data-sql-server-and-revoscaler-tutorial"></a>对新数据进行评分 (SQL Server 和 RevoScaleR 教程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本课程是有关如何在 SQL Server 中使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)的[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的一部分。

在此步骤中, 您将使用在上一课中创建的逻辑回归模型来对另一个使用与输入相同的独立变量的数据集进行评分。

> [!div class="checklist"]
> * 对新数据进行评分
> * 创建评分的直方图

> [!NOTE]
> 对于其中一些步骤, 你需要 DDL 管理员权限。

## <a name="generate-and-save-scores"></a>生成并保存分数
  
1. 更新 sqlScoreDS 数据源 (在第[2 课](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)中创建), 以使用在上一课中创建的列信息。
  
    ```R
    sqlScoreDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlScoreTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
2. 若要确保不会丢失结果, 请创建新的数据源对象。 然后, 使用新的数据源对象在 RevoDeepDive 数据库中填充新表。
  
    ```R
    sqlServerOutDS <- RxSqlServerData(table = "ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead )
    ```
    此时尚未创建表。 此语句仅定义数据的容器。
     
3. 如果需要, 请使用**rxGetComputeContext ()** 检查当前计算上下文, 并将计算上下文设置为服务器。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
4. 作为预防措施, 请检查输出表是否存在。 如果已存在具有相同名称的, 则尝试写入新表时, 将会出现错误。
  
    若要执行此操作，请调用函数 [rxSqlServerTableExists](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable) 和 [rxSqlServerDropTable](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsqlserverdroptable)，传递表名称作为输入。
  
    ```R
    if (rxSqlServerTableExists("ccScoreOutput"))     rxSqlServerDropTable("ccScoreOutput")
    ```
  
    + **rxSqlServerTableExists**查询 ODBC 驱动程序, 如果表存在, 则返回 TRUE, 否则返回 FALSE。
    + **rxSqlServerDropTable**执行 DDL, 如果成功删除表, 则返回 TRUE, 否则返回 FALSE。

5. 执行[rxPredict](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxpredict)以创建评分, 并将其保存在数据源 sqlScoreDS 中定义的新表中。
  
    ```R
    rxPredict(modelObject = logitObj,
        data = sqlScoreDS,
        outData = sqlServerOutDS,
        predVarNames = "ccFraudLogitScore",
          type = "link",
        writeModelVars = TRUE,
        overwrite = TRUE)
    ```
  
    rxPredict 函数是另一种函数，支持在远程计算上下文中运行。 您可以使用**rxPredict**函数基于[rxLinMod](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlinmod)、 [rxLogit](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxlogit)或[rxGlm](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxglm)从模型创建分数。
  
    - 参数 *writeModelVars* 在此处设置为 **TRUE** 。 这意味着新表中将包含用于估计的变量。
  
    - 参数 *predVarNames* 指定将在其中存储结果的变量。 在此, `ccFraudLogitScore`你要传递一个新变量。
  
    - rxPredict 的 type 参数定义计算预测的方式。 指定关键字**响应**以根据响应变量的小数位数生成分数。 或者使用关键字**链接**基于基础链接函数生成分数, 在这种情况下, 将使用逻辑刻度创建预测。

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

创建新表后, 计算并显示10000预测分数的直方图。 如果指定下限值和上限值, 计算速度会更快, 因此从数据库获取这些值, 并将它们添加到工作数据。

1. 创建一个新的数据源 sqlMinMax, 该数据源查询数据库以获取低值和较高值。
  
    ```R
    sqlMinMax <- RxSqlServerData(
        sqlQuery = paste("SELECT MIN(ccFraudLogitScore) AS minVal,",
        "MAX(ccFraudLogitScore) AS maxVal FROM ccScoreOutput"),
        connectionString = sqlConnString)
    ```

     从本示例中，可以看到使用 RxSqlServerData 数据源对象根据 SQL 查询、函数或存储过程定义任意数据集，然后将其用于 R 代码中非常容易。 变量不会存储实际值，只存储数据源定义；仅当在函数（如 rxImport）中使用此查询时，才会执行此查询以生成该值。
      
2. 调用[rxImport](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rximport)函数以将值放置在可跨计算上下文共享的数据帧中。
  
    ```R
    minMaxVals <- rxImport(sqlMinMax)
    minMaxVals <- as.vector(unlist(minMaxVals))
    ```

    **结果**
     
    ```R
    > minMaxVals
     
    [1] -23.970256   9.786345
    ```

3. 由于最大值和最小值可用, 因此请使用这些值为生成的分数创建另一个数据源。
  
    ```R
    sqlOutScoreDS <- RxSqlServerData(sqlQuery = "SELECT ccFraudLogitScore FROM ccScoreOutput",
        connectionString = sqlConnString,
        rowsPerRead = sqlRowsPerRead,
            colInfo = list(ccFraudLogitScore = list(
                low = floor(minMaxVals[1]),
                        high = ceiling(minMaxVals[2]) ) ) )
    ```

4. 使用数据源对象 sqlOutScoreDS 可获取分数, 计算并显示直方图。 添加代码以根据需要设置计算上下文。
  
    ```R
    # rxSetComputeContext(sqlCompute)
    rxHistogram(~ccFraudLogitScore, data = sqlOutScoreDS)
    ```
  
    **结果**
  
    ![R 创建的复杂直方图](media/rsql-sue-complex-histogram.png "R 创建的复杂直方图")
  
## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 R 转换数据](../../advanced-analytics/tutorials/deepdive-transform-data-using-r.md)