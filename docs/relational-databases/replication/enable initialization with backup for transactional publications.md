---
title: "使用备份来初始化事务发布 (SQL Server Management Studio) | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "手动初始化订阅 [SQL Server 复制]"
  - "订阅 [SQL Server 复制], 初始化"
  - "初始化订阅 [SQL Server 复制], 无快照"
  - "事务复制, 备份和还原"
  - "备份 [SQL Server 复制], 事务复制"
ms.assetid: 9df00514-aa9d-4ac6-9766-d226c9958175
caps.latest.revision: 30
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
---
# 使用备份来初始化事务发布 (SQL Server Management Studio)
  若要使用备份初始化对事务发布的订阅，请启用发布以允许使用备份进行初始化，然后指定创建订阅时的备份信息：  
  
-   在启用发布 **订阅选项** 页 **发布属性-\< 发布>** 对话框。 有关访问此对话框的详细信息，请参阅 [View and Modify Publication Properties](../../relational-databases/replication/publish/view-and-modify-publication-properties.md)。  
  
-   使用存储过程中指定的备份信息 [sp_addsubscription & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-addsubscription-transact-sql.md)。 有关所需的参数详细信息 **sp_addsubscription**, ，请参阅 [初始化事务订阅从备份和 #40;复制 TRANSACT-SQL 编程 & #41;](../../relational-databases/replication/initialize a transactional subscription from a backup.md)。  
  
### 启用使用备份来初始化  
  
1.  在 **订阅选项** 页 **发布属性-\< 发布>** 对话框中，选择一个值的 **True** 为 **允许从备份文件初始化** 选项。  
  
## 另请参阅  
 [初始化事务订阅（不使用快照）](../../relational-databases/replication/initialize-a-transactional-subscription-without-a-snapshot.md)  
  
  