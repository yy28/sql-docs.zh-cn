---
title: "使用 R 可视化 SQL Server 数据（对数据科学的深入探讨） | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
applies_to: 
  - "SQL Server 2016"
dev_langs: 
  - "R"
ms.assetid: 10def0b3-9b09-4df9-b8aa-69516f7d7659
caps.latest.revision: 14
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
---
# 使用 R 可视化 SQL Server 数据（对数据科学的深入探讨）
[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 中的增强包包括多个具有很好的可伸缩性和非常适用于并行处理的函数。 通常这些函数带有前缀 *rx* 或 *Rx*。  
  
在本演练中，使用 rxHistogram 函数查看 _creditLine_ 列中值的分布（按性别）。  
  
## 使用 rxHistogram 和 rxCube 可视化数据  
  
1.  使用以下 R 代码来调用 *rxHistogram* 函数并传递公式和数据源。 可首先在本地运行，查看预期的结果以及需要的时间。
  
    ```R  
    rxHistogram(~creditLine|gender, data = sqlFraudDS,  histType = "Percent")   
    ```  
 
    在内部，rxHistogram 调用 rxCube 函数，它包含在 **RevoScaleR** 包中。 rxCube 函数输出一个列表（或数据帧），其中包括针对公式中指定的每个变量的一个列和一个计数列。
    
2. 现在，将计算上下文设置为远程 SQL Server 计算机并再次运行 *rxHistogram*。
  
    ```R  
    rxSetComputeContext(sqlCompute)  
    ```  
 
3.    因为你使用的是相同的数据源，所以结果是完全相同的；但是计算是在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上执行的。  结果将返回到本地工作站用于绘图。  
   
![histogram results](../../advanced-analytics/r-services/media/rsql-sue-histogramresults.jpg "histogram results")  

  
4.  还可调用 *rxCube* 函数，并将结果传递到 R 绘制函数。  例如，对于 numTrans 和 numIntlTrans 的每个组合，以下示例使用 rxCube 计算 fraudRisk 的平均值：  
  
    ```R  
    cube1 <- rxCube(fraudRisk~F(numTrans):F(numIntlTrans),  data = sqlFraudDS)   
    ```  
  
    若要指定用于计算组均值的组，请使用 `F()` 表示法。 在本示例中，`F(numTrans):F(numIntlTrans)` 表明变量 _numTrans_和 _numIntlTrans_ 中的整数应视为类别变量，并且每个整数值都有一个级别。  
  
    由于低级别和高级别已添加到数据源 sqlFraudDS（使用 colInfo 参数），因此在直方图中将自动使用级别。  
  
5.  rxCube 的返回值默认为表示交叉表的 rxCube object 对象。 但是，可以使用 rxResultsDF 函数将结果转换为一个数据帧，该数据帧可轻松用于 R 的一个标准绘图函数。  
  
    ```R  
    cubePlot <- rxResultsDF(cube1)   
    ```  
  
    > [!TIP]  
    > 请注意，rxCube** 函数包含一个可选参数，returnDataFrame** = TRUE，该参数可用于将结果直接转换成数据帧。 例如：  
    >   
    > `print(rxCube(fraudRisk~F(numTrans):F(numIntlTrans), data = sqlFraudDS, returnDataFrame = TRUE))`  
    >   
    > 但是，rxResultsDF 的输出更加清晰，并保留了源列的名称。  
  
6.  最后，通过运行以下代码，使用来自所有 R 分发版中包含的 lattice 包的 levelplot 函数创建热图。  
  
    ```R  
    levelplot(fraudRisk~numTrans*numIntlTrans, data = cubePlot)   
    ```  
  
    **结果**  
  
    ![scatterplot results](../../advanced-analytics/r-services/media/rsql-sue-scatterplotresults.jpg "scatterplot results")  
  
即使从上面的快速分析中也可以看出欺诈风险随事务数量和国际事务数量的增加而增高。

有关 *rxCube* 函数的详细信息和常规交叉表的详细信息，请参阅[数据摘要](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries)。  
  
## 下一步  
[创建模型（对数据科学的深入探讨）](../../advanced-analytics/r-services/create-models-data-science-deep-dive.md)  
  
## 上一步  
[第 2 课：创建和运行 R 脚本（对数据科学的深入探讨）](../../advanced-analytics/r-services/lesson-2-create-and-run-r-scripts-data-science-deep-dive.md)  
  
## 另请参阅  
[对数据科学的深入探讨：使用 RevoScaleR 包](../../advanced-analytics/r-services/data-science-deep-dive-using-the-revoscaler-packages.md)  
  
  
  
