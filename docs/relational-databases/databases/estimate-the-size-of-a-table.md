---
title: "估计表的大小 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "database-engine"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "页 [SQL Server], 空间"
  - "空间 [SQL Server], 表"
  - "行大小 [SQL Server]"
  - "大小 [SQL Server], 表"
  - "列大小 [SQL Server]"
  - "预测表的大小 [SQL Server]"
  - "表大小 [SQL Server]"
  - "估计表的大小"
  - "聚集索引, 表大小"
  - "磁盘空间 [SQL Server], 表"
  - "空间分配 [SQL Server], 表大小"
  - "设计数据库 [SQL Server], 估计大小"
  - "每页保留的可用行数 [SQL Server]"
  - "计算表的大小"
ms.assetid: 15c17c92-616f-402e-894b-907a296efe5f
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 30
---
# 估计表的大小
  可以使用下列步骤估计在表中存储数据所需的空间：  
  
1.  按照[估计堆的大小](../../relational-databases/databases/estimate-the-size-of-a-heap.md)或[估计聚集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)中的说明来计算堆或聚集索引所需空间。  
  
2.  对于每个非聚集索引，按照[估计非聚集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)中的说明来计算其所需空间。  
  
3.  对步骤 1 和步骤 2 中计算的值求和。  
  
## 另请参阅  
 [估计数据库的大小](../../relational-databases/databases/estimate-the-size-of-a-database.md)   
 [估计堆的大小](../../relational-databases/databases/estimate-the-size-of-a-heap.md)   
 [估计聚集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-clustered-index.md)   
 [估计非聚集索引的大小](../../relational-databases/databases/estimate-the-size-of-a-nonclustered-index.md)  
  
  