---
title: "发布服务器属性 - 发布服务器，发布数据库 | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- replication
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.rep.configdistwizard.pubproperties.pubdb.f1
helpviewer_keywords:
- Publisher Properties dialog box
ms.assetid: 574ea2e7-4e7b-4733-ab52-429ca93c7b0a
caps.latest.revision: 21
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: cc86424019df085038fffd9b076576eb9c717024
ms.lasthandoff: 04/11/2017

---
# <a name="publisher-properties---publisher-publication-databases"></a>发布服务器属性 - 发布服务器，发布数据库
  通过使用 **“发布服务器属性”** 对话框的 **“发布数据库”** 页， **sysadmin** 固定服务器角色中的用户可以启用数据库以进行复制。 启用数据库并不会发布相应的数据库；不过，该数据库的 **db_owner** 固定数据库角色中的所有用户都可以对该数据库创建一个或多个发布。  
  
## <a name="options"></a>选项  
 **事务性**  
 选中此复选框后， **db_owner** 固定数据库角色中的用户将可以在数据库中创建快照发布或事务发布。  
  
 **合并**  
 选中此复选框后， **db_owner** 固定数据库角色中的用户将可以在数据库中创建合并发布。  
  
## <a name="see-also"></a>另请参阅  
 [查看和修改分发服务器和发布服务器属性](../../relational-databases/replication/view-and-modify-distributor-and-publisher-properties.md)   
 [属性参考（复制）](../../relational-databases/replication/properties-reference-replication.md)  
  
  
