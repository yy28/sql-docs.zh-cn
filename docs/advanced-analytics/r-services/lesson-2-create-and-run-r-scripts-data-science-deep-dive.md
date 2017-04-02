---
title: "第 2 课：创建和运行 R 脚本（对数据科学的深入探讨） | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "10/26/2016"
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
ms.assetid: 51e8e66f-a0a5-4e96-aa71-f5c870e6d0d4
caps.latest.revision: 18
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 18
---
# 第 2 课：创建和运行 R 脚本（对数据科学的深入探讨）
设置数据源并建立一个或多个计算上下文之后，现在可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 运行一些高性能的 R 脚本。  在本课程中，将使用服务器计算上下文执行一些常见的机器学习任务：  
  
-   可视化数据并生成一些摘要统计信息    
-   创建线性回归模型    
-   创建逻辑回归模型    
-   对新数据进行评分并创建分数直方图  
  
## 更改服务器的计算上下文  
运行任何 R 代码前，需要指定当前或活动计算上下文。  
  
1.  若要激活已经使用 R 定义了的计算上下文，请使用 rxSetComputeContext 函数，如下所示：  
  
    ```R  
    rxSetComputeContext(sqlCompute)   
    ```  
  
    运行此语句后，会在 *sqlCompute* 参数中指定的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上进行所有后续计算。  
  
  
2.  如果决定在工作站上运行 R 代码，可以使用  **local** 关键字将计算上下文切换回本地计算机。  
  
    ```R  
    rxSetComputeContext ("local")    
    ```  
  
    有关此函数支持的其他关键字的列表，请从 R 命令行键入 `help("rxSetComputeContext")` 。  
  
> [!NOTE]  
> 指定了计算上下文后，在更改前，它将保持活动状态。 但是，任何无法在远程服务器上下文中运行的 R 脚本都将在本地运行。  
  
## 计算摘要统计信息  
若要查看计算上下文的工作原理，请尝试使用 *sqlFraudDS* 数据源生成一些摘要统计信息。  请记住，数据源对象只是定义你将使用的数据，而不会更改计算上下文。

+ 若要在本地执行 summary，请使用 *rxSetComputeContext* 并指定“local”关键字。
+ 若要在 SQL Server 计算机上创建相同的计算，切换到前面定义的 SQL 计算上下文。  

  
1.  调用 *rxSummary* 函数并传递所需的参数（如公式和数据源）并将结果分配给变量 *sumOut*。  
  
    ```R  
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)  
  
    ```  
  
    R 语言提供了许多 summary 函数，但 rxSummary 支持在各种远程计算上下文上执行，包括 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。  有关类似函数的详细信息，请参阅 [ScaleR 引用](https://msdn.microsoft.com/microsoft-r/scaler/scaler)中的[数据摘要](https://msdn.microsoft.com/microsoft-r/scaler-user-guide-data-summaries)。
  
2.  处理完成后，可将 sumOut 变量中的内容打印到控制台。  
  
    ```R  
    sumOut  
    ```  
  
    > [!NOTE]  
    > 请勿在结果从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机返回前尝试进行打印，否则可能会遇到错误。  
  
  
**结果**  
  
*Summary Statistics Results for: ~gender + balance + numTrans +*   
 *numIntlTrans + creditLine*    
 *Data: sqlFraudDS (RxSqlServerData Data Source)*    
 *Number of valid observations: 10000*    
 *Name  Mean    StdDev  Min Max ValidObs    MissingObs*    
 *balance       4075.0318 3926.558714            0   25626 100000*    
 *numTrans        29.1061   26.619923 0     100 10000    0           100000*    
 *numIntlTrans     4.0868    8.726757 0      60 10000    0           100000*    
 *creditLine       9.1856    9.870364 1      75 10000    0          100000 Category Counts for gender*    
 *Number of categories: 2*    
 *Number of valid observations: 10000*   
 *Number of missing observations: 0*    
 *gender Counts*    
 *Male   6154*    
  *Female 3846*  
  
## 添加最大值和最小值  
根据计算的摘要统计信息，你会发现一些有用的数据信息，可以将这些数据放入数据源，以备日后进一步计算使用。 例如，最小值和最大值可用于计算直方图，因此可以将高值和低值添加到 RxSqlServerData 数据源。  
  
幸运的是，[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)] 包含的优化函数可以非常高效地将整数数据转换成分类因素数据。  
  
1.  首先设置一些临时变量。  
  
    ```R  
    sumDF <- sumOut$sDataFrame   
    var <- sumDF$Name    
    ```  
  
2.  使用之前创建的变量 ccColInfo 定义数据源中的列。  
  
    还需添加一些新的计算列（numTrans、numIntlTrans 和 creditLine）到列集合。  
  
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
  
3.  更新列集合后，可以应用以下语句创建之前定义的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据源的更新版本。  
  
    ```R  
    sqlFraudDS <- RxSqlServerData(  
        connectionString = sqlConnString,   
        table = sqlFraudTable,   
        colInfo = ccColInfo,        
        rowsPerRead = sqlRowsPerRead)   
    ```  
  
    现在，sqlFraudDS 数据源包括添加到 ccColInfo 的新列。  
  
所做的修改仅影响 R 中的数据源对象；未向数据库表写入任何新数据。 但是，可使用在 *sumOut* 变量中捕获的数据来创建可视化效果和摘要。 下一步，学习如何在切换计算上下文时执行此操作。 

> [!TIP]
> 如果忘记了使用的是哪个计算上下文，请使用 `rxGetComputeContext()`。  如果返回值是 `RxLocalSeq Compute Context`，则使用的是本地计算上下文。
  
## 下一步  
[使用 R 可视化 SQL Server 数据（对数据科学的深入探讨）](../../advanced-analytics/r-services/visualize-sql-server-data-using-r-data-science-deep-dive.md)  
  
## 上一步  
[定义并使用计算上下文（对数据科学的深入探讨）](../../advanced-analytics/r-services/define-and-use-compute-contexts-data-science-deep-dive.md)  
  
  
  
