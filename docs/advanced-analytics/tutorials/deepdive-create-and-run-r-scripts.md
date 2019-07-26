---
title: 计算汇总统计信息 RevoScaleR 教程
description: 本教程演示如何使用 R 语言在 SQL Server 上计算统计摘要统计信息。
ms.prod: sql
ms.technology: machine-learning
ms.date: 11/27/2018
ms.topic: tutorial
author: dphansen
ms.author: davidph
ms.openlocfilehash: 5b1ec344a2ec9728a24d45c47dd80737e6155b01
ms.sourcegitcommit: 9062c5e97c4e4af0bbe5be6637cc3872cd1b2320
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68469816"
---
# <a name="compute-summary-statistics-in-r-sql-server-and-revoscaler-tutorial"></a>R 中的计算汇总统计信息 (SQL Server 和 RevoScaleR 教程)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

本课程是有关如何在 SQL Server 中使用[RevoScaleR 函数](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)的[RevoScaleR 教程](deepdive-data-science-deep-dive-using-the-revoscaler-packages.md)的一部分。

它使用在前面的课程中创建的已建立数据源和计算上下文来运行此脚本中的高功率 R 脚本。 在本课中, 您将使用本地和远程服务器计算上下文执行以下任务:

> [!div class="checklist"]
> * 将计算上下文切换到 SQL Server
> * 获取有关远程数据对象的摘要统计信息
> * 计算本地摘要

如果已完成前面的课程, 应具有以下远程计算上下文: sqlCompute 和 sqlComputeTrace。 前进后, 在后续课程中, 你将使用 sqlCompute 和本地计算上下文。

在本课程中, 使用 R IDE 或**rgui.exe**运行 r 脚本。

## <a name="compute-summary-statistics-on-remote-data"></a>计算有关远程数据的汇总统计信息

你需要指定远程计算上下文, 然后才能远程运行任何 R 代码。 所有后续计算都在*sqlCompute*参数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]中指定的计算机上进行。

计算上下文将保持活动状态, 直到您对其进行更改。 但是,*不能*在远程服务器上下文中运行的任何 R 脚本都将在本地自动运行。

若要查看计算上下文的工作原理, 请在远程 SQL Server 上的 sqlFraudDS 数据源上生成汇总统计信息。 此数据源对象是在第[2 课](deepdive-create-sql-server-data-objects-using-rxsqlserverdata.md)中创建的, 表示 RevoDeepDive 数据库中的 ccFraudSmall 表。 

1. 将计算上下文切换为在上一课中创建的 sqlCompute:
  
    ```R
    rxSetComputeContext(sqlCompute)
    ```

2. 调用[rxSummary](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxsummary)函数并传递所需的参数, 如公式和数据源, 并将结果分配给变量`sumOut`。
  
    ```R
    sumOut <- rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlFraudDS)
    ```
  
    R 语言提供了许多汇总功能, 但**RevoScaleR**中的**rxSummary**支持对各种远程计算上下文执行, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]其中包括。 有关类似函数的信息, 请参阅[使用 RevoScaleR 的数据摘要](https://docs.microsoft.com/machine-learning-server/r/how-to-revoscaler-data-summaries)。
  
3. 将 sumOut 的内容打印到控制台。
  
    ```R
    sumOut
    ```
    > [!NOTE]
    > 如果遇到错误, 请等待几分钟, 然后再重试命令。

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
  
2. 从 SQL Server 提取数据时, 可以通过增加为每个读取提取的行数来获得更好的性能, 假设内存中可以容纳增加的块大小。 运行以下命令, 增加数据源上的*rowsPerRead*参数的值。 之前，rowsPerRead 的值设置为 5000。
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```

3. 对新数据源调用**rxSummary** 。
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
   实际结果应与在 **计算机的上下文中运行** rxSummary [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的结果相同。 但是，该操作可能更快，也可能更慢。 因为正在将数据传输到本地计算机进行分析，因此操作很大程度取决于数据库的连接。

4. 切换回远程计算上下文以进行后续几课。

    ```R
    rxSetComputeContext(sqlCompute)
    ```

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 R 可视化 SQL Server 数据](../../advanced-analytics/tutorials/deepdive-visualize-sql-server-data-using-r.md)