---
title: "为复制启用数据库 (SQL Server Management Studio) | Microsoft Docs"
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
  - "数据库 [SQL Server 复制]"
ms.assetid: 8092faa3-9cff-4f81-926c-6a0070d1ce2c
caps.latest.revision: 33
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 33
---
# 为复制启用数据库 (SQL Server Management Studio)
  当 **sysadmin** 固定服务器角色的成员使用新建发布向导创建发布时，将为复制隐式启用数据库。 成员 **sysadmin** 固定的服务器角色还可以启用对数据库进行复制显式，以便属于 **db_owner** 固定的数据库角色可以在该数据库中创建一个或多个发布。 若要显式启用数据库，请使用 **发布数据库** 页 **发布服务器属性-\< 发布服务器>** 对话框。 有关访问此对话框的详细信息，请参阅 [Create a Publication](../../relational-databases/replication/publish/create-a-publication.md)。  
  
### 为复制启用数据库  
  
1.  在 **发布数据库** 页 **发布服务器属性-\< 发布服务器>** 对话框中，选择 **事务性** 和/或 **合并** 您想要复制的每个数据库的复选框。 选择 **“事务”** 将为快照复制启用数据库。  
  
2.  [!INCLUDE[clickOK](../../includes/clickok-md.md)]  
  
  