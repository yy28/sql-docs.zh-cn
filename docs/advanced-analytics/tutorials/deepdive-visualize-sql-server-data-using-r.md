---
title: " 实现使用 R （SQL 和 R 深入） 的 SQL Server 数据可视化效果 |Microsoft 文档"
ms.date: 12/14/2017
ms.reviewer: 
ms.suite: sql
ms.prod: machine-learning-services
ms.prod_service: machine-learning-services
ms.component: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: tutorial
applies_to:
- SQL Server 2016
- SQL Server 2017
dev_langs: R
ms.assetid: 10def0b3-9b09-4df9-b8aa-69516f7d7659
caps.latest.revision: "14"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 77321589a87230535502cc37a75bf09722abb66d
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
#  <a name="visualize-sql-server-data-using-r-sql-and-r-deep-dive"></a>实现使用 R （SQL 和 R 深入） 的 SQL Server 数据可视化效果

本文是有关如何使用数据科学深入了解教程的一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的增强包包括多个具有很好的可伸缩性和非常适用于并行处理的函数。 通常这些函数带有前缀 **rx** 或 **Rx**。

对于本演练中，你使用**rxHistogram**函数以查看中的值的分布_creditLine_按性别划分的列。

## <a name="visualize-data-using-rxhistogram"></a>实现使用 rxHistogram 的数据可视化效果

1. 使用以下 R 代码来调用 [rxHistogram](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxhistogram) 函数并传递公式和数据源。 可首先在本地运行，查看预期的结果以及需要的时间。
  
    ```R
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")
    ```
 
    在内部，**rxHistogram** 调用 [rxCube](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxcube) 函数，它包含在 **RevoScaleR** 包中。 **rxCube**加上计数列输出包含一列以指定在公式中，每个变量进行单个列表 （或数据帧）。
    
2. 现在，将计算上下文设置为远程 SQL Server 计算机并运行**rxHistogram**试。
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
 
3. 因为你使用的是相同的数据源，所以结果是完全相同的；但是计算是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上执行的。  结果将返回到本地工作站用于绘图。
   
![直方图结果](media/rsql-sue-histogramresults.jpg "直方图结果")

4. 你还可以调用**rxCube**函数并将结果传递给 R 绘制函数。  例如，对于 numTrans  和 numIntlTrans  的每个组合，以下示例使用 rxCube  计算 fraudRisk 的平均值：
  
    ```R
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)
    ```
  
    若要指定用于计算组均值的组，请使用 `F()` 表示法。 在此示例中，`F(numTrans):F(numIntlTrans)`指示变量中的整数`_numTrans`和`numIntlTrans`应被视为分类变量，与每个整数值的级别。
  
    因为低和高级别已添加到数据源`sqlFraudDS`(使用`colInfo`参数)，级别将自动使用直方图中。
  
5. 默认值返回的值**rxCube**是*rxCube 对象*，它表示交叉表。 但是，可以使用 [rxResultsDF](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxresultsdf) 函数将结果转换为一个数据帧，该数据帧可轻松用于 R 的一个标准绘图函数。
  
    ```R
    cubePlot <- rxResultsDF(cube1)
    ```
  
    **RxCube**函数包含一个可选参数， *returnDataFrame* = **TRUE**，是无法使用以将结果直接转换为数据帧。 例如：
    
    `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`
       
    但是，rxResultsDF  的输出更加清晰，并保留了源列的名称。
  
6. 最后，运行以下代码以创建热度地图使用`levelplot`函数从**格状**包，其中所有 R 分发版附带了。
  
    ```R
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)
    ```
  
    **结果**
  
    ![散点图结果](media/rsql-sue-scatterplotresults.jpg "散点图结果")
  
即使从上面的快速分析中也可以看出欺诈风险随事务数量和国际事务数量的增加而增高。

有关详细信息**rxCube**函数和交叉表通常情况下，请参阅[使用 RevoScaleR 的数据摘要](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)。

## <a name="next-step"></a>下一步

[创建 R 模型使用 SQL Server 数据](../../advanced-analytics/tutorials/deepdive-create-models.md)

## <a name="previous-step"></a>上一步

[创建并运行 R 脚本](../../advanced-analytics/tutorials/deepdive-create-and-run-r-scripts.md)
