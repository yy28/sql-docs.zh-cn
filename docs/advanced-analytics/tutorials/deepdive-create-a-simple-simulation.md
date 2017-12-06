---
title: "第 5 课：创建简单模拟（对数据科学的深入探讨）| Microsoft Docs"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: f420b816-ddab-4a1a-89b9-c8285a2d33a3
caps.latest.revision: "16"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e5dfca8ecef324b510b614ae93b7aefe9a4efe07
ms.sourcegitcommit: 531d0245f4b2730fad623a7aa61df1422c255edc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/01/2017
---
# <a name="create-a-simple-simulation"></a>创建简单的模拟

到目前为止您一直使用 R 函数旨在专门用于转移数据之间[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和本地计算上下文。 但是，假设编写了自己的自定义 R 函数，并且想要在服务器上下文中运行它呢？

通过使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] rxExec **函数，可以在** 计算机的上下文中调用任意函数。 你可以使用 rxExec 以显式将工作分摊在单个服务器节点中的内核。

本课程中，使用远程服务器来创建简单模拟。 模拟不需要任何[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据; 该示例仅演示了如何设计自定义的函数，然后调用它使用 rxExec 函数。

有关使用 rxExec 的更复杂示例，请参阅此文章：[粗粒度使用并行 foreach 和 rxExec](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)

## <a name="create-the-function"></a>创建函数

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
  
2.  若要模拟单个掷骰子游戏，则运行该函数。
  
    ```R
    rollDice()
    ```
  
    你是胜了还是败了？
  
现在看一下可如何多次运行函数，创建有助于确定获胜概率的模拟。

## <a name="create-the-simulation"></a>创建模拟

若要运行的上下文中的任意函数[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算机，你调用 rxExec 函数。 尽管 rxExec 还支持分布式的函数执行并行跨节点或在服务器上下文中的内核，此处你将使用它只是为了在服务器上运行你的自定义函数。

1. 作为 rxExec，以及修改模拟的某些其他参数的自变量调用自定义的函数。
  
    ```R
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")
    length(sqlServerExec)
    ```
  
    - 使用 timesToRun 参数，指示执行函数的次数。  在这种情况下，将掷 20 次骰子。
  
    - 可使用 RNGseed 和 RNGkind 参数控制随机数的生成。 将 RNGseed 设置为“自动”时，会在每个辅助角色上初始化并行随机数流。
  
2. RxExec 函数创建具有每次运行; 的一个元素的列表但是，不会看到多发生情况的完成列表之前。 所有迭代都完成后，以 `length` 开头的行将返回一个值。
  
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
  
>  [!TIP]
> 
> 如果你想要使用这些方法使用 1000 万个观测值的更大的数据集进行试验，都可以从 Revolution analytics 网站数据文件：[索引的数据集](http://packages.revolutionanalytics.com/datasets)
>   
> 若要重新使用较大的数据文件使用本演练，下载数据，然后对每个数据源，如下所示修改：
>  - 将 ccFraudCsv 和 ccScoreCsv 变量设置为指向新的数据文件
>  - 将 sqlFraudTable 中引用的表名称更改为 ccFraud10
>  - 将 sqlScoreTable 中引用的表名称更改为 ccFraudScore10

## <a name="previous-step"></a>上一步

[SQL Server 和 XDF 文件之间移动数据](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)


