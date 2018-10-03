---
title: SQL Server 使用 R 可视化数据 （SQL 和 R 的深入探讨） |Microsoft Docs
ms.prod: sql
ms.technology: machine-learning
ms.date: 04/15/2018
ms.topic: tutorial
author: HeidiSteen
ms.author: heidist
manager: cgronlun
ms.openlocfilehash: 0d34ece68c421dbb7aabd845e117c9f07e00d013
ms.sourcegitcommit: 2420c57d2952add3697dbe0467ee1d755c5c2ee5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/26/2018
ms.locfileid: "47217512"
---
#  <a name="visualize-sql-server-data-using-r-sql-and-r-deep-dive"></a>SQL Server 使用 R 可视化数据 （SQL 和 R 的深入探讨）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是有关如何使用数据科学的深入教程的一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的增强包包括多个具有很好的可伸缩性和非常适用于并行处理的函数。 通常这些函数带有前缀 **rx** 或 **Rx**。

对于本演练中，你使用**rxHistogram**函数查看中的值分布_creditLine_按性别划分的列。

## <a name="visualize-data-using-rxhistogram"></a>使用 rxHistogram 可视化数据

1. 使用以下 R 代码来调用 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) 函数并传递公式和数据源。 可首先在本地运行，查看预期的结果以及需要的时间。
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    在内部，**rxHistogram** 调用 [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) 函数，它包含在 **RevoScaleR** 包中。 **rxCube**输出一个列表 （或数据帧） 包含在公式中，指定每个变量的一列和一个计数列。
    
2. 现在，将计算上下文设置为远程 SQL Server 计算机并运行**rxHistogram**试。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
 
3. 因为你使用的是相同的数据源，所以结果是完全相同的；但是计算是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上执行的。  结果将返回到本地工作站用于绘图。
   
![直方图结果](media/rsql-sue-histogramresults.jpg "直方图结果")

4. 您还可以调用**rxCube**函数，并将结果传递到 R 绘制函数。  例如，对于 numTrans  和 numIntlTrans  的每个组合，以下示例使用 rxCube  计算 fraudRisk 的平均值：
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    若要指定用于计算组均值的组，请使用 `F()` 表示法。 在此示例中，`F(numTrans):F(numIntlTrans)`指示变量中的整数`numTrans`和`numIntlTrans`应视为类别变量，并且每个整数值的级别。
  
    由于低和高级别已添加到数据源`sqlFraudDS`(使用`colInfo`参数)，在直方图中会自动使用级别。
  
5. 默认返回值**rxCube**是*rxCube 对象*，它表示交叉表。 但是，可以使用 [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) 函数将结果转换为一个数据帧，该数据帧可轻松用于 R 的一个标准绘图函数。
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    **RxCube**函数将包含一个可选参数， *returnDataFrame* = **TRUE**，可用于将结果直接转换成数据帧。 例如：
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    但是，rxResultsDF  的输出更加清晰，并保留了源列的名称。
  
6. 最后，运行以下代码以创建热度地图使用`levelplot`函数从**点阵**包，其中包含所有 R 分发版。
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **结果**
  
    ![散点图结果](media/rsql-sue-scatterplotresults.jpg "散点图结果")
  
即使从上面的快速分析中也可以看出欺诈风险随事务数量和国际事务数量的增加而增高。

有关详细信息**rxCube**函数和交叉表一般情况下，请参阅[使用 RevoScaleR 的数据摘要](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)。

## <a name="next-step"></a>下一步

[创建使用 SQL Server 数据的 R 模型](../../advanced-analytics/tutorials/deepdive-create-models.md)

## <a name="previous-step"></a>上一步

[创建并运行 R 脚本](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
