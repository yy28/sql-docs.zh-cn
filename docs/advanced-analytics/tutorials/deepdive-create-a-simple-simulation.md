---
title: "创建简单的模拟 （SQL 和 R 深入） |Microsoft 文档"
ms.custom: 
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
ms.assetid: f420b816-ddab-4a1a-89b9-c8285a2d33a3
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: cgronlund
ms.workload: Inactive
ms.openlocfilehash: 047ce5984129eadde9ef92505b7c5448f7c37d4f
ms.sourcegitcommit: 23433249be7ee3502c5b4d442179ea47305ceeea
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/20/2017
---
# <a name="create-a-simple-simulation-sql-and-r-deep-dive"></a>创建简单的模拟 （SQL 和 R 深入）

本文是在数据科学深入教程中，如何使用中的最后一步[RevoScaleR](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/revoscaler)与 SQL Server。

到目前为止您一直使用 R 函数旨在专门用于转移数据之间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和本地计算上下文。 但是，假设编写了自己的自定义 R 函数，并且想要在服务器上下文中运行它呢？

通过使用 [rxExec](https://docs.microsoft.com/machine-learning-server/r-reference/revoscaler/rxexec) 函数，可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机的上下文中调用任意函数。 你还可以使用**rxExec**以显式将工作分摊分布在一台服务器中的核心。

在本课程中，你可以使用远程服务器来创建简单的模拟。 模拟不需要任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据；示例仅演示如何设计自定义函数，然后使用 rxExec 函数调用该函数。

有关使用的更复杂示例**rxExec**，请参阅此文章：[粗粒度使用并行 foreach 和 rxExec](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)

## <a name="create-the-custom-function"></a>创建自定义函数

常见的赌场游戏包含掷两枚骰子，规则如下：

- 如果第一次掷时掷到了 7 或 11，则胜。
- 如果掷到 2、3 或 12，则败。
- 如果掷到 4、5、6、8、9 或 10，则该点数成为你的分数，然后继续掷，直至再次掷出这个分数（这种情况下为胜），或掷出 7（这种情况下为败）。

通过创建自定义函数，然后多次运行该函数便可轻松在 R 中模拟此游戏。

1.  使用以下 R 代码创建自定义函数：
  
    ```R
    rollDice <- function()
    {
        result <- NULL
        point <- NULL
        count <- 1
            while (is.null(result))
            {
                roll <- sum(sample(6, 2, replace=TRUE))
  
                if (is.null(point))
                { point <- roll }
                if (count == 1 && (roll == 7 || roll == 11))
                {  result <- "Win" }
                else if (count == 1 && (roll == 2 || roll == 3 || roll == 12))
                { result \<- "Loss" }
                else if (count > 1 && roll == 7 )
                { result \<- "Loss" }
                else if (count > 1 && point == roll)
                { result <- "Win" }
                else { count <- count + 1 }
            }
            result
    }
    ```
  
2.  若要模拟掷单个游戏，运行该函数。
  
    ```R
    rollDice()
    ```
  
    你是胜了还是败了？
  
现在让我们看一下如何可以使用**rxExec**多次运行该函数，以创建模拟，可帮助确定一种成功的概率。

## <a name="create-the-simulation"></a>创建模拟

若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上下文中运行任意函数，可以调用 rxExec 函数。 尽管**rxExec**还在节点之间并行支持分布式的函数执行或核心数在服务器上下文中，此处其 SQL Server 计算机上运行您的自定义函数。

1. 自定义函数作为自变量调用**rxExec**连同修改模拟其他参数。
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    - 使用 timesToRun 参数，指示执行函数的次数。  在这种情况下，将掷 20 次骰子。
  
    - 可使用 RNGseed 和 RNGkind 参数控制随机数的生成。 将 RNGseed 设置为“自动”时，会在每个辅助角色上初始化并行随机数流。
  
2. rxExec 函数会创建一个列表，其中一次运行一个元素；但是，在列表完成前，不会看到太多操作执行。 所有迭代都完成后，以 `length` 开头的行将返回一个值。
  
    然后可以转到下一步，获得输赢记录的汇总。
  
3. 将返回的列表转换为使用 R 的向量`unlist`函数，并汇总使用对结果`table`函数。
  
    ```R
    table(unlist(sqlServerExec))
    ```
  
    结果应如下所示：
  
     *丢失 Win* *12 8*

## <a name="conclusions"></a>结论

通过本教程，应已熟练以下这些任务：
  
-   获取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据用于分析
  
-   在 R 中创建和修改数据源
  
-   在工作站和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务器之间传递模型、数据和绘图
  

如果你想要使用这些方法使用 1000 万个观测值的更大的数据集进行试验，都可以从 Revolution analytics 网站数据文件：[索引的数据集](http://packages.revolutionanalytics.com/datasets)

若要重新使用较大的数据文件使用本演练，下载数据，然后对每个数据源，如下所示修改：

1. 修改变量`ccFraudCsv`和`ccScoreCsv`使其指向新的数据文件
2. 更改中引用的表的名称*sqlFraudTable*到`ccFraud10`
3. 更改中引用的表的名称*sqlScoreTable*到`ccFraudScore10`

## <a name="additional-samples"></a>其他示例

现在，您已掌握了计算上下文和 RevoScaler 函数来传递和转换数据的使用，请查看以下教程：

[机器学习服务的 R 教程](machine-learning-services-tutorials.md)
## <a name="previous-step"></a>上一步

[在 SQL Server 和 XDF 文件之间移动数据](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)
