---
title: "创建和运行 R 脚本 （SQL 和 R 深入） |Microsoft 文档"
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
dev_langs:
- R
ms.assetid: 51e8e66f-a0a5-4e96-aa71-f5c870e6d0d4
caps.latest.revision: 
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 1ca2c7227163816092e7248fe20cb377fc03ac03
ms.sourcegitcommit: 99102cdc867a7bdc0ff45e8b9ee72d0daade1fd3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/11/2018
---
# <a name="create-and-run-r-scripts-sql-and-r-deep-dive"></a>创建和运行 R 脚本 （SQL 和 R 深入）
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本文是有关如何使用数据科学深入了解教程的一部分[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

设置数据源并建立一个或多个计算上下文之后，现在可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]运行一些高性能的 R 脚本。  在本课程中，你使用 server 计算上下文执行一些常见的机器学习任务：

- 可视化数据并生成一些摘要统计信息
- 创建线性回归模型
- 创建逻辑回归模型
- 对新数据进行评分并创建分数直方图

## <a name="change-compute-context-to-the-server"></a>更改计算到服务器的上下文

运行任何 R 代码前，需要指定当前或活动计算上下文。

1. 若要激活已经使用 R 定义了的计算上下文，请使用 rxSetComputeContext 函数，如下所示：
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```
  
    就会立即运行此语句时，所有后续计算上进行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中指定的计算机*sqlCompute*参数。
  
2. 如果决定在工作站上运行 R 代码，可以使用  **local** 关键字将计算上下文切换回本地计算机。
  
    ```R
    rxSetComputeContext ("local")
    ```
  
    有关此函数支持的其他关键字的列表，请从 R 命令行键入 `help("rxSetComputeContext")` 。
  
3. 指定了计算上下文后，在更改前，它将保持活动状态。 但是，任何无法在远程服务器上下文中运行的 R 脚本都将在本地运行。

## <a name="compute-some-summary-statistics"></a>计算某些摘要统计信息

若要查看计算上下文的工作原理，请尝试生成一些摘要统计信息使用`sqlFraudDS`数据源。  请记住，数据源对象只需定义使用; 的数据它不会更改计算上下文。

+ 若要执行本地的摘要，使用**rxSetComputeContext**并指定_本地_关键字。
+ 若要在 SQL Server 计算机上创建相同的计算，切换到前面定义的 SQL 计算上下文。

1. 调用[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary)函数并传递所需的自变量，如公式和数据源，并将结果赋给变量`sumOut`。
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    R 语言提供了许多摘要函数，但**rxSummary**上各种远程计算上下文，包括支持执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关类似的功能的信息，请参阅[使用 RevoScaleR 的数据摘要](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)。
  
2. 处理完成后，你可以打印的内容`sumOut`变量到控制台。
  
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

 *creditLine       9.1856    9.870364 1      75 10000    0          100000*

 *性别的类别计数*

 *Number of categories: 2*

 *Number of valid observations: 10000*

 *Number of missing observations: 0*

 *gender Counts*

 *Male   6154*

  *Female 3846*

## <a name="add-maximum-and-minimum-values"></a>添加最大和最小值

根据计算的摘要统计信息，你会发现一些有用的数据信息，可以将这些数据放入数据源，以备日后进一步计算使用。 例如，可以使用最小和最大值来计算直方图。 为此，让我们添加高和低值**RxSqlServerData**数据源。

幸运的是[!INCLUDE[rsql_productname](../../includes/rsql-productname-md.md)]包括可以有效地将整数数据转换为分类因素数据的优化的功能。

1. 首先设置一些临时变量。
  
    ```R
    sumDF <- sumOut$sDataFrame
    var <- sumDF$Name
    ```
  
2. 使用之前创建的变量 `ccColInfo` 定义数据源中的列。
  
    此外，将添加一些新计算列 (`numTrans`， `numIntlTrans`，和`creditLine`) 到列集合。
  
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
  
3. 具有更新列集合中，应用以下语句以创建的更新的版本[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]前面定义的数据源。
  
    ```R
    sqlFraudDS <- RxSqlServerData(
        connectionString = sqlConnString,
        table = sqlFraudTable,
        colInfo = ccColInfo,
        rowsPerRead = sqlRowsPerRead)
    ```
  
    `sqlFraudDS`数据源现在包括新列添加使用`ccColInfo`。
  

此时，修改影响仅数据源中的对象 R;任何新的数据具有尚未写入到数据库表。 但是，你可以使用在捕获的数据`sumOut`变量来创建可视化效果和摘要。 在下一步中，您将学习如何执行此操作时切换计算上下文。

> [!TIP]
> 如果你忘记了你正在使用哪些计算上下文，运行`rxGetComputeContext()`。  "RxLocalSeq 计算上下文"的返回值指示运行本地计算上下文中。

## <a name="next-step"></a>下一步

[使用 R 可视化 SQL Server 数据](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)

## <a name="previous-step"></a>上一步

[定义并使用计算上下文](../../advanced-analytics/tutorials/deepdive-define-and-use-compute-contexts.md)
