---
title: 发布服务器属性 - 发布服务器，发布数据库 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
f1_keywords:
- sql12.rep.configdistwizard.pubproperties.pubdb.f1
helpviewer_keywords:
- Publisher Properties dialog box
ms.assetid: 574ea2e7-4e7b-4733-ab52-429ca93c7b0a
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 11e3913b05ac8f595422b74ef4e0d098a593e3cb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48216077"
---
# <a name="publisher-properties---publisher-publication-databases"></a>发布服务器属性 - 发布服务器，发布数据库
  通过使用 **“发布服务器属性”** 对话框的 **“发布数据库”** 页， **sysadmin** 固定服务器角色中的用户可以启用数据库以进行复制。 启用数据库并不会发布相应的数据库；不过，该数据库的 **db_owner** 固定数据库角色中的所有用户都可以对该数据库创建一个或多个发布。  
  
## <a name="options"></a>选项  
 **事务性**  
 选中此复选框后， **db_owner** 固定数据库角色中的用户将可以在数据库中创建快照发布或事务发布。  
  
 **合并**  
 选中此复选框后， **db_owner** 固定数据库角色中的用户将可以在数据库中创建合并发布。  
  
## <a name="see-also"></a>请参阅  
 [查看和修改分发服务器和发布服务器属性](view-and-modify-distributor-and-publisher-properties.md)   
 [属性参考（复制）](properties-reference-replication.md)  
  
  
