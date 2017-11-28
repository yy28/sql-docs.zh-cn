---
title: "分析本地计算上下文中的数据 |Microsoft 文档"
ms.custom: 
ms.date: 05/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: r-services
ms.tgt_pltfrm: 
ms.topic: article
applies_to: SQL Server 2016
dev_langs: R
ms.assetid: 787bb526-4a13-40fa-9343-75d3bf5ba6a2
caps.latest.revision: "13"
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 514cc855af010347006054ad30fc5e5c36b16322
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/09/2017
---
# <a name="analyze-data-in-local-compute-context-data-science-deep-dive"></a>分析本地计算上下文 （数据科学深入了解） 中的数据

尽管它可能更快地是若要运行使用服务器上下文的复杂 R 代码，有时它是只是更方便地获取你的数据外[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]和对其在专用的工作站上进行分析。

本部分将介绍如何切换回本地计算上下文中，以及在上下文之间移动数据优化性能。

## <a name="create-a-local-summary"></a>创建本地摘要

1. 更改计算上下文，以在本地完成所有工作。
  
    ```R
    rxSetComputeContext ("local")
    ```
  
2. 从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提取数据时，通常可以通过增加每次读取所提取的行数获得更好的性能。  若要执行此操作，在数据源上增加 rowsPerRead 参数的值。
  
    ```R
    sqlServerDS1 <- RxSqlServerData(
       connectionString = sqlConnString,
       table = sqlFraudTable,
       colInfo = ccColInfo,
       rowsPerRead = 10000)
    ```
  
    之前，rowsPerRead 的值设置为 5000。
  
3. 现在，调用新数据源上的 **rxSummary** 。
  
    ```R
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)
    ```
  
    实际结果应为相同的上下文中运行 rxSummary 时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]计算机。  但是，该操作可能更快，也可能更慢。 因为正在将数据传输到本地计算机进行分析，因此操作很大程度取决于数据库的连接。


## <a name="next--step"></a>下一步

[SQL Server 和 XDF 文件之间移动数据](../../advanced-analytics/tutorials/deepdive-move-data-between-sql-server-and-xdf-file.md)

## <a name="previous-step"></a>上一步

[执行使用 rxDataStep 分块分析](../../advanced-analytics/tutorials/deepdive-perform-chunking-analysis-using-rxdatastep.md)


