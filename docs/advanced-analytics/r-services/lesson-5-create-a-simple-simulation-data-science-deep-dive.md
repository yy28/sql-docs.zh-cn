---
title: "第 5 课：创建简单模拟（对数据科学的深入探讨） | Microsoft Docs"
ms.custom: ""
ms.date: "10/03/2016"
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
ms.assetid: f420b816-ddab-4a1a-89b9-c8285a2d33a3
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 15
---
# 第 5 课：创建简单模拟（对数据科学的深入探讨）
目前为止，一直使用的是 SQL Server R Services 提供的专门用于在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 和本地计算上下文之间移动数据的 R 函数。 但是，假设编写了自己的自定义 R 函数，并且想要在服务器上下文中运行它呢？  
  
通过使用 *rxExec* 函数，可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机的上下文中调用任意函数。 还可以使用 rxExec 将工作显式分布给单个服务器节点中的内核。  
  
本课程中，使用远程服务器来创建简单模拟。 模拟不需要任何 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据；示例仅演示如何设计自定义函数，然后使用 rxExec 函数调用该函数。  
  
有关更复杂的使用 rxExec 的示例，请参阅此文章：[http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html](http://blog.revolutionanalytics.com/2015/04/coarse-grain-parallelism-with-foreach-and-rxexec.html)  
  
## 创建函数  
常见的赌场游戏包含掷两枚骰子，规则如下：  
  
-   如果第一次掷时掷到了 7 或 11，则胜。  
  
-   如果掷到 2、3 或 12，则败。  
  
-   如果掷到 4、5、6、8、9 或 10，则该点数成为你的分数，然后继续掷，直至再次掷出这个分数（这种情况下为胜），或掷出 7（这种情况下为败）。  
  
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
                { result <- "Loss" }    
                else if (count > 1 && roll == 7 )   
                { result <- "Loss" }    
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
  
## 创建模拟  
若要在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机上下文中运行任意函数，可以调用 rxExec 函数。 尽管 rxExec 也支持在服务器上下文的节点或内核之间并行分布式执行函数，但此处仅将其用于在服务器上运行自定义函数。  
  
1.  调用自定义函数作为到 rxExec 的参数，以及修改模拟的某些其他参数。  
  
    ```R  
    sqlServerExec <- rxExec(rollDice, timesToRun=20, RNGseed="auto")   
    length(sqlServerExec)   
    ```  
  
    -   使用 timesToRun 参数，指示执行函数的次数。  在这种情况下，将掷 20 次骰子。  
  
    -   可使用 RNGseed 和 RNGkind 参数控制随机数的生成。 将 RNGseed 设置为“自动”时，会在每个辅助角色上初始化并行随机数流。  
  
2.  rxExec 函数会创建一个列表，其中一次运行一个元素；但是，在列表完成前，不会看到太多操作执行。 所有迭代都完成后，以 `length` 开头的行将返回一个值。  
  
    然后可以转到下一步，获得输赢记录的汇总。  
  
3.  使用 R 的 unlist 函数将返回的列表转换为向量，并使用 table 函数汇总结果。  
  
    ```R  
    table(unlist(sqlServerExec))  
    ```  
  
    结果应如下所示：  
  
     *败  胜*   
     *12  8*  
  
## 结论  
通过本教程，应已熟练以下这些任务：  
  
-   获取 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 数据用于分析  
  
-   在 R 中创建和修改数据源  
  
-   在工作站和 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 服务器之间传递模型、数据和绘图  
  
>  [!TIP]
> 
> 如果要使用更大的数据集（1000 万个观测值）体验这些技术，可以从 [http://packages.revolutionanalytics.com/datasets](http://packages.revolutionanalytics.com/datasets) 获取数据文件。  
>   
> 若要通过更大的数据文件重新使用此演练，只需下载数据并修改数据源，如下所示：   
>  -   将 ccFraudCsv 和 ccScoreCsv 变量设置为指向新的数据文件     
>  -   将 sqlFraudTable 中引用的表名称更改为 ccFraud10    
>  -   将 sqlScoreTable 中引用的表名称更改为 ccFraudScore10   
  
## 上一步  
[在 SQL Server 和 XDF 文件之间移动数据（对数据科学的深入探讨）](../../advanced-analytics/r-services/move-data-between-sql-server-and-xdf-file-data-science-deep-dive.md)  
  
  
  
