---
title: "发布服务器属性 - 发布服务器，发布数据库 | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.rep.configdistwizard.pubproperties.pubdb.f1"
helpviewer_keywords: 
  - "“发布服务器属性”对话框"
ms.assetid: 574ea2e7-4e7b-4733-ab52-429ca93c7b0a
caps.latest.revision: 21
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 21
---
# 发布服务器属性 - 发布服务器，发布数据库
  通过使用 **“发布服务器属性”** 对话框的 **“发布数据库”** 页， **sysadmin** 固定服务器角色中的用户可以启用数据库以进行复制。 启用数据库不会将发布该数据库;相反，它允许任何用户 **db_owner** 该数据库中创建一个或多个发布数据库上的固定的数据库角色。  
  
## 选项  
 **事务性**  
 选中此复选框可允许用户在 **db_owner** 固定的数据库角色都可以在数据库中创建快照发布或事务发布。  
  
 **合并**  
 选中此复选框可允许用户在 **db_owner** 固定的数据库角色在数据库中创建合并发布。  
  
## 另请参阅  
 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [& #40; 属性引用复制和 #41;](../../relational-databases/replication/properties-reference-replication.md)  
  
  