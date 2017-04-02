---
title: "发布数据库 | Microsoft Docs"
ms.custom: ""
ms.date: "03/03/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.newpubwizard.publicationdatabase.f1"
ms.assetid: a9fafc9b-9963-4b59-97a0-3472158fa665
caps.latest.revision: 23
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 23
---
# 发布数据库
  发布数据库是发布服务器上的数据库，它是要复制的数据和数据库对象的源。 必须启用复制操作中使用的每个发布数据库。 当 **sysadmin** 固定服务器角色成员执行以下任一操作时，即可启用相应的数据库：  
  
-   使用新建发布向导对该数据库创建发布。  
  
-   在 **“发布服务器属性”** 对话框中选择该数据库。  
  
-   执行 **sp_replicationdboption** 和设置选项 **发布** （对于快照发布或事务发布） 或 **合并发布** （对于合并发布） 到 **True**。  
  
## 选项  
 **“数据库”**  
 选择包含要发布的数据和数据库对象的数据库名称。  
  
## 另请参阅  
 [发布数据和数据库对象](../../relational-databases/replication/publish/publish-data-and-database-objects.md)   
 [创建发布](../../relational-databases/replication/publish/create-a-publication.md)   
 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [sp_replicationdboption & #40;Transact SQL & #41;](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)  
  
  