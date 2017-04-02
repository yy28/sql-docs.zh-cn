---
title: "设置排队更新冲突解决选项 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "冲突解决 [SQL Server 复制]，排队更新订阅"
  - "排队更新订阅 [SQL Server 复制]"
ms.assetid: bb6b6c71-42c7-421a-a0fa-d5594d27e35d
caps.latest.revision: 34
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 34
---
# 设置排队更新冲突解决选项 (SQL Server Management Studio)
  设置冲突解决选项对于支持排队更新订阅上的发布 **订阅选项** 页 **发布属性-\< 发布>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
### 设置排队更新冲突解决选项  
  
1.  在 **订阅选项** 页 **发布属性-\< 发布>** 对话框中，选择以下值之一的 **冲突解决策略** 选项︰  
  
    -   **保留发布服务器更改**  
  
    -   **保留订阅服务器更改**  
  
    -   **重新初始化订阅**  
  
2.  [!INCLUDE[clickOK](../../../includes/clickok-md.md)]  
  
## 另请参阅  
 [允许更新事务发布的订阅](../../../relational-databases/replication/publish/enable-updating-subscriptions-for-transactional-publications.md)   
 [排队更新冲突的检测和解决](../../../relational-databases/replication/transactional/queued-updating-conflict-detection-and-resolution.md)  
  
  