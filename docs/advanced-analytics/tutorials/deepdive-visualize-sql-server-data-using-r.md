---
title: 使用 RevoScaleR rxHistogram-SQL Server 机器学习的 SQL Server 数据可视化
description: 有关如何实现 SQL Server 上使用 R 语言的数据可视化效果的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 4092de07d19d4d33bd56025076e606269c2b04e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "67962157"
---
#  <a name="visualize-sql-server-data-using-r-sql-server-and-revoscaler-tutorial"></a>SQL Server 使用 R 可视化数据 （SQL Server 和 RevoScaleR 教程）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程中属于[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

在本课程中，使用 R 函数查看中的值分布*creditLine*按性别划分的列。

> [!div class="checklist"]
> * 创建直方图输入的最小最大变量
> * 实现在直方图中使用的数据可视化效果**rxHistogram**从**RevoScaleR**
> * 使用散点图使用可视化**levelplot**从**点阵**包含在基础 R 发行版

如本课程中所示，可以组合使用同一个脚本中的开源和 Microsoft 专用函数。

## <a name="add-maximum-and-minimum-values"></a>添加最大和最小值

根据上一课中的计算摘要统计信息，你已经可以插入到进行进一步计算的数据源的数据有关的一些有用信息。 例如，最小和最大值可用于计算直方图。 在此练习中，将添加到的最高价和最值**RxSqlServerData**数据源。

1. 首先设置一些临时变量。
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. 使用变量*ccColInfo*数据源中定义的列在上一课中创建。
  
   添加新的计算的列 (*numTrans*， *numIntlTrans*，并*creditLine*) 到重写原始定义的列集合。 下面的脚本将基于从 sumOut，获取该存储的内存中输出的最小值和最大值的因素**rxSummary**。 
  
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
  
3. 更新列集合中，应用以下语句创建的更新的版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]前面定义的数据源。
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    SqlFraudDS 数据源现在包括新列添加了 using *ccColInfo*。
  
此时，所做的修改仅影响的数据源对象中 R;任何新数据包含尚未写入到数据库表。 但是，sumOut 变量中捕获的数据可用于创建可视化效果和摘要。 

> [!TIP]
> 如果你忘记了您正在使用哪个计算上下文，运行**rxGetComputeContext()** 。 "RxLocalSeq 计算上下文"的返回值指示运行本地计算上下文中。

## <a name="visualize-data-using-rxhistogram"></a>使用 rxHistogram 可视化数据

1. 使用以下 R 代码来调用 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) 函数并传递公式和数据源。 可首先在本地运行，查看预期的结果以及需要的时间。
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    在内部，**rxHistogram** 调用 [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) 函数，它包含在 **RevoScaleR** 包中。 **rxCube**输出一个列表 （或数据帧） 包含在公式中，指定每个变量的一列和一个计数列。
    
2. 现在，将计算上下文设置为远程 SQL Server 计算机并运行**rxHistogram**试。
  
    ```R
    rxSetComputeContext(sqlCompute)
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
3. 结果是完全相同，因为正在使用相同的数据源，但在第二个步骤中，在远程服务器上执行计算。 结果将返回到本地工作站用于绘图。
   
  ![直方图结果](media/rsql-sue-histogramresults.jpg "直方图结果")


## <a name="visualize-with-scatter-plots"></a>使用散点图进行可视化

散点图通常在数据浏览过程用于比较两个变量之间的关系。 可以为此，请使用内置的 R 包，使用所提供的输入**RevoScaleR**函数。

1. 调用[rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcrosstabs)函数来计算的平均值*fraudRisk*的每个组合*numTrans*并*numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    若要指定用于计算组均值的组，请使用 `F()` 表示法。 在此示例中，`F(numTrans):F(numIntlTrans)`指示变量中的整数`numTrans`和`numIntlTrans`应视为类别变量，并且每个整数值的级别。
  
    默认返回值**rxCube**是*rxCube 对象*，它表示交叉表。 
  
2. 调用[rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf)函数将结果转换成可轻松用于 R 的一个标准绘图函数之一的数据帧。
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    **RxCube**函数将包含一个可选参数， *returnDataFrame* = **TRUE**，可用于将结果直接转换成数据帧。 例如：
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    但是的输出**rxResultsDF**清晰，并保留了源列的名称。 你可以运行`head(cube1)`跟`head(cubePlot)`以输出进行比较。
  
3. 创建热度地图使用**levelplot**函数从**点阵**包，包括所有 R 分发版。
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **结果**
  
    ![散点图结果](media/rsql-sue-scatterplotresults.jpg "散点图结果")
  
从上面的快速分析，可以看出欺诈风险随事务数和国际事务数。

有关详细信息**rxCube**函数和交叉表一般情况下，请参阅[使用 RevoScaleR 的数据摘要](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [创建使用 SQL Server 数据的 R 模型](../../advanced-analytics/tutorials/deepdive-create-models.md)