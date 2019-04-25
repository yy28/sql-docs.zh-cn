---
title: 计算摘要统计信息 RevoScaleR 教程-SQL Server 机器学习
description: 有关如何计算统计摘要统计信息在 SQL Server 上使用 R 语言的教程演练。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
manager: cgronlun
ms.openlocfilehash: 883a4afa68571c18e6dcaffe96d12644f611f99a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "62641332"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>计算 R （SQL Server 和 RevoScaleR 教程） 中的摘要统计信息
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

本课程中属于[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)如何使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

它使用建立的数据源和在前面的课程中创建的计算上下文来运行在本视频中的高性能的 R 脚本。 在本课中，将使用本地和远程服务器计算上下文，执行以下任务：

> [!div class="checklist"]
> * 将计算上下文切换到 SQL Server
> * 获取对远程数据对象的摘要统计信息
> * 计算本地摘要

如果已完成前面的课程，您应具有这些远程计算上下文： sqlCompute 和 sqlComputeTrace。 下一步，您使用将 sqlCompute 和本地计算上下文在后续课程中。

使用 R IDE 或**Rgui**在本课程中运行 R 脚本。

## <a name="compute-summary-statistics-on-remote-data"></a>计算对远程数据的摘要统计信息

你可以远程运行的任何 R 代码之前，需要指定在远程计算上下文。 所有后续计算发生[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中指定的计算机*sqlCompute*参数。

在更改之前，计算上下文保持活动状态。 但是，任何 R 脚本*不能*运行在远程服务器上下文中的将自动在本地运行。

若要查看计算上下文的工作原理，请生成 sqlFraudDS 数据源在远程 SQL 服务器上的摘要统计信息。 此数据源对象中创建[第 2 课](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)和表示 RevoDeepDive 数据库中的 ccFraudSmall 表。 

1. 切换到 sqlCompute 在上一课中创建计算上下文：
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. 调用[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary)函数并传递所需的参数，如公式和数据源，并将结果分配给变量`sumOut`。
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    R 语言提供了许多 summary 函数，但**rxSummary**中**RevoScaleR**支持在各种远程计算上下文，包括执行[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]。 有关类似函数的信息，请参阅[使用 RevoScaleR 的数据摘要](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)。
  
3. 打印到控制台 sumOut 的内容。
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > 如果遇到错误，等待几分钟时间完成，然后重试该命令的执行。

**结果**

```R
Summary Statistics Results for: ~gender + balance + numTrans + numIntlTrans + creditLine
Data: sqlFraudDS (RxSqlServerData Data Source)
Number of valid observations: 10000

 Name  Mean    StdDev  Min Max ValidObs    MissingObs
 balance       4075.0318 3926.558714            0   25626 100000
 numTrans        29.1061   26.619923 0     100 10000    0           100000
 numIntlTrans     4.0868    8.726757 0      60 10000    0           100000
 creditLine       9.1856    9.870364 1      75 10000    0          100000
 
 Category Counts for gender
 Number of categories: 2
 Number of valid observations: 10000
 Number of missing observations: 0

 gender Counts
  Male   6154
  Female 3846
```

## <a name="create-a-local-summary"></a>创建本地摘要

1. 更改计算上下文，以在本地完成所有工作。
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. 当从 SQL Server 中提取数据，通常就可以更好的性能通过增加为每次读取中提取的行数假定增加的块大小可以容纳在内存中。 运行以下命令，以增加的值*rowsPerRead*上数据源的参数。 之前，rowsPerRead 的值设置为 5000。
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. 调用**rxSummary**上新的数据源。
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
   实际结果应与在 **计算机的上下文中运行** rxSummary [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的结果相同。 但是，该操作可能更快，也可能更慢。 因为正在将数据传输到本地计算机进行分析，因此操作很大程度取决于数据库的连接。

4. 切换回远程计算上下文的下一步的几个课程。

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 R 可视化 SQL Server 数据](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)