---
title: "第 4 课：在本地计算上下文中分析数据（对数据科学的深入探讨） | Microsoft Docs"
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
ms.assetid: 787bb526-4a13-40fa-9343-75d3bf5ba6a2
caps.latest.revision: 13
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# 第 4 课：在本地计算上下文中分析数据（对数据科学的深入探讨）
虽然通常情况下使用服务器上下文运行复杂 R 代码更快，但有时候从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 外获取数据并在专用工作站上对其进行分析会更方便。  
  
本部分将介绍如何切换回本地计算上下文中，以及在上下文之间移动数据优化性能。  
  
## 创建本地摘要  
  
1.  更改计算上下文，以在本地完成所有工作。  
  
    ```R  
    rxSetComputeContext ("local")    
    ```  
  
2.  从 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 提取数据时，通常可以通过增加每次读取所提取的行数获得更好的性能。  若要执行此操作，在数据源上增加 rowsPerRead 参数的值。  
  
    ```R  
    sqlServerDS1 <- RxSqlServerData(  
       connectionString = sqlConnString,        
       table = sqlFraudTable,   
       colInfo = ccColInfo,   
       rowsPerRead = 10000)  
    ```  
  
    之前，rowsPerRead 的值设置为 5000。  
  
3.  现在，调用新数据源上的 *rxSummary*。  
  
    ```R  
    rxSummary(formula = ~gender + balance + numTrans + numIntlTrans + creditLine, data = sqlServerDS1)    
    ```  
  
    实际结果应与在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 计算机的上下文中运行 *rxSummary* 的结果相同。  但是，该操作可能更快，也可能更慢。 因为正在将数据传输到本地计算机进行分析，因此操作很大程度取决于数据库的连接。  
  

## 下一步  
[在 SQL Server 和 XDF 文件之间移动数据（对数据科学的深入探讨）](../../advanced-analytics/r-services/move-data-between-sql-server-and-xdf-file-data-science-deep-dive.md)  
  
## 上一步  
[使用 rxDataStep 执行区块分析（对数据科学的深入探讨）](../../advanced-analytics/r-services/perform-chunking-analysis-using-rxdatastep-data-science-deep-dive.md)  
  
  
  
