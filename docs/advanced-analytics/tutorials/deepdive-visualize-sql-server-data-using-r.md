---
title: 使用 RevoScaleR rxHistogram 可视化 SQL Server 数据
description: 有关如何使用 R 语言在 SQL Server 中实现数据可视化的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 210fade2820c53ba585043827e7e3d2c36315319
ms.sourcegitcommit: c1382268152585aa77688162d2286798fd8a06bb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/19/2019
ms.locfileid: "68344652"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>使用 R 可视化 SQL Server 数据 (SQL Server 和 RevoScaleR 教程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程是有关如何在 SQL Server 中使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)的[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的一部分。

在本课程中, 使用 R 函数查看按性别划分的*creditLine*列中值的分布。

> [!div class="checklist"]
> * 创建直方图输入的最小值-最大值变量
> * 使用**rxHistogram**从**RevoScaleR**直观显示直方图中的数据
> * 使用**levelplot**从**点阵**中包含的散点图可视化

如本课程所示, 可以在同一脚本中合并开源和 Microsoft 特定函数。

## <a name="add-maximum-and-minimum-values"></a>添加最大值和最小值

根据上一课中计算得出的汇总统计信息, 您已经发现了一些有用的信息, 您可以将这些数据插入到数据源中以供进一步计算。 例如, 最小值和最大值可用于计算直方图。 在此练习中, 将高值和低值添加到**RxSqlServerData**数据源。

1. 首先设置一些临时变量。
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. 使用在上一课中创建的变量*ccColInfo*来定义数据源中的列。
  
   向重写原始定义的列集合添加新的计算列 (*numTrans*、 *numIntlTrans*和*creditLine*)。 下面的脚本根据从 sumOut 获取的最小值和最大值 (从**rxSummary**存储内存中输出) 来添加因子。 
  
    ```R 
    ccColInfo <- list(
        gender = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Male", "Female")),
        cardholder = list(type = "factor",
          levels = c("1", "2"), 
          newLevels = c("Principal", "Secondary")), 
        state = list(type = "factor", 
          levels = as.character(1:51), 
          newLevels = stateAbb), 
        balance  = list(type = "numeric"),
        numTrans = list(type = "factor", 
          levels = as.character(sumDF[var == "numTrans", "Min"]:sumDF[var == "numTrans", "Max"])),
        numIntlTrans = list(type = "factor",  
            levels = as.character(sumDF[var == "numIntlTrans", "Min"]:sumDF[var =="numIntlTrans", "Max"])),
        creditLine = list(type = "numeric")
            )
    ```
  
3. 更新列集合后, 应用以下语句以创建之前定义的[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据源的更新版本。
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    SqlFraudDS 数据源现在包括使用*ccColInfo*添加的新列。
  
此时, 修改仅影响 R 中的数据源对象;尚未向数据库表写入新数据。 但是, 可以使用 sumOut 变量中捕获的数据创建可视化效果和摘要。 

> [!TIP]
> 如果忘记了正在使用的计算上下文, 请运行**rxGetComputeContext ()** 。 如果返回值为 "RxLocalSeq 计算上下文", 则表示您正在本地计算上下文中运行。

## <a name="visualize-data-using-rxhistogram"></a>使用 rxHistogram 实现数据的可视化

1. 使用以下 R 代码来调用 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) 函数并传递公式和数据源。 可首先在本地运行，查看预期的结果以及需要的时间。
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    在内部，**rxHistogram** 调用 [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) 函数，它包含在 **RevoScaleR** 包中。 **rxCube**输出一个列表 (或数据帧), 其中包含在公式中指定的每个变量的一个列和一个计数列。
    
2. 现在, 将计算上下文设置为远程 SQL Server 计算机, 然后再次运行**rxHistogram** 。
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. 结果完全相同, 因为你使用的是相同的数据源, 但在第二个步骤中, 将在远程服务器上执行计算。 结果将返回到本地工作站用于绘图。
   
  ![直方图结果](media/rsql-sue-histogramresults.jpg "直方图结果")


## <a name="visualize-with-scatter-plots"></a>用散点图可视化

散点图通常在数据浏览过程中用于比较两个变量之间的关系。 你可以使用内置 R 包实现此目的, 并使用**RevoScaleR**函数提供的输入。

1. 调用[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs)函数为*numTrans*和*numIntlTrans*的每个组合计算*fraudRisk*的平均值:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    若要指定用于计算组均值的组，请使用 `F()` 表示法。 在此示例中`F(numTrans):F(numIntlTrans)` , 指示变量`numTrans`中的整数和`numIntlTrans`应视为分类变量, 并且每个整数值都有一个级别。
  
    **RxCube**的默认返回值是一个*rxCube 对象*, 该对象表示一个交叉表。 
  
2. 调用[rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf)函数可将结果转换为一个数据帧, 该数据帧可轻松用于 R 的一个标准绘图函数。
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    **RxCube**函数包含一个可选参数*returnDataFrame* = **TRUE**, 可用于将结果直接转换为数据帧。 例如：
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    但是, **rxResultsDF**的输出为整洁, 并保留源列的名称。 您可以`head(cube1)` `head(cubePlot)`随后运行来比较输出。
  
3. 使用**点阵**包中的**levelplot**函数创建热度地图, 其中包含所有 R 分发版。
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **结果**
  
    ![散点图结果](media/rsql-sue-scatterplotresults.jpg "散点图结果")
  
在此快速分析中, 你可以看到, 诈骗风险增加, 同时增加了事务数和国际事务数。

有关**rxCube**函数和交叉表的详细信息, 请参阅[使用 RevoScaleR 的数据摘要](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 SQL Server 数据创建 R 模型](../../advanced-analytics/tutorials/deepdive-create-models.md)