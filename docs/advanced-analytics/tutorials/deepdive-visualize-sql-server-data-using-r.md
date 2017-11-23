---
title: "使用 R 直观地显示 SQL Server 数据（对数据科学的深入探讨）| Microsoft Docs"
ms.custom: SQL2016_New_Updated
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 10def0b3-9b09-4df9-b8aa-69516f7d7659
caps.latest.revision: "14"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a67480daf011a021002e1688b006a1f0593f8e5f
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="visualize-sql-server-data-using-r"></a>使用 R 可视化 SQL Server 数据

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的增强包包括多个具有很好的可伸缩性和非常适用于并行处理的函数。 通常这些函数带有前缀 *rx* 或 *Rx*。

在本演练中，使用 rxHistogram  函数查看 _creditLine_ 列中值的分布（按性别）。

## <a name="visualize-data-using-rxhistogram"></a>实现使用 rxHistogram 的数据可视化效果

1. 使用以下 R 代码来调用 rxHistogram 函数并传递公式和数据源。 可首先在本地运行，查看预期的结果以及需要的时间。
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    在内部，rxHistogram 调用 rxCube 函数，它包括在**RevoScaleR**包。 RxCube 函数输出加上计数列包含一列以指定在公式中，每个变量进行单个列表 （或数据帧）。
    
2. 现在，将计算上下文设置为远程 SQL Server 计算机，并再次运行 rxHistogram。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
 
3. 因为你使用的是相同的数据源，所以结果是完全相同的；但是计算是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上执行的。  结果将返回到本地工作站用于绘图。
   
![直方图结果](media/rsql-sue-histogramresults.jpg "直方图结果")

4. 此外可以调用 rxCube 函数，并将结果传递给 R 绘图函数。  例如，下面的示例使用 rxCube 来计算的平均值*fraudRisk*对每个组合*numTrans*和*numIntlTrans*:
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    若要指定用于计算组均值的组，请使用 `F()` 表示法。 在本示例中， `F(numTrans):F(numIntlTrans)` 表明变量 _numTrans_ 和 _numIntlTrans_ 中的整数应视为类别变量，并且每个整数值都有一个级别。
  
    由于低级别和高级别已添加到数据源 sqlFraudDS  （使用 colInfo  参数），因此在直方图中将自动使用级别。
  
5. RxCube 的返回值是默认情况下*rxCube 对象*，它表示交叉表。 但是，可以使用 rxResultsDF  函数将结果转换为一个数据帧，该数据帧可轻松用于 R 的一个标准绘图函数。
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    > [!TIP]
    > 
    > 请注意，rxCube 函数包括一个可选参数， *returnDataFrame* = TRUE，你可以使用将结果直接转换为数据帧。 例如：
    >   
    > `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
    >   
    > 但是，rxResultsDF 的输出更清楚，并保留源列的名称。
  
6. 最后，运行以下代码以创建热度地图使用`levelplot`函数从**格状**包，其中所有 R 分发版附带了。
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **结果**
  
    ![散点图结果](media/rsql-sue-scatterplotresults.jpg "散点图结果")
  
即使从上面的快速分析中也可以看出欺诈风险随事务数量和国际事务数量的增加而增高。

有关 rxCube 函数和通常交叉表的详细信息，请参阅[数据摘要](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries)。

## <a name="next-step"></a>下一步

[创建模型](../../advanced-analytics/tutorials/deepdive-create-models.md)

## <a name="previous-step"></a>上一步

[第 2 课：创建并运行 R 脚本](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)


