---
title: "拖放路由 (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- DROP ROUTE
- DROP_ROUTE_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- dropping routes
- DROP ROUTE statement
- deleting routes
- routes [Service Broker], removing
- removing routes
ms.assetid: d8fab0bc-d54a-46ca-9437-552db7477d40
caps.latest.revision: 
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f63dbf4868d0b1add92d0971a11eaab0fb7a6629
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2018
---
# <a name="drop-route-transact-sql"></a>DROP ROUTE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除路由，并从当前数据库的路由表中删除该路由的信息。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
DROP ROUTE route_name  
[ ; ]  
```  
  
## <a name="arguments"></a>参数  
 *route_name*  
 要删除的路由名称。 不能指定服务器、数据库和架构名称。  
  
## <a name="remarks"></a>注释  
 存储的路由的路由表是可以读取通过目录视图的元数据表**sys.routes**。 路由表只能通过 CREATE ROUTE、ALTER ROUTE 和 DROP ROUTE 语句进行更新。  
  
 对于一个路由，无论是否有会话使用它，都可以删除它。 不过，如果没有到远程服务的其他路由，则这些会话的消息将保留在传输队列中，直到创建了到远程服务的路由或会话超时为止。  
  
## <a name="permissions"></a>权限  
 删除路由的权限默认授予该路由的所有者、db_ddladmin 或 db_owner 固定数据库角色的成员和 sysadmin 固定服务器角色的成员。  
  
## <a name="examples"></a>示例  
 下面的示例将删除 `ExpenseRoute` 路由。  
  
```  
DROP ROUTE ExpenseRoute ;  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER 路由 &#40;Transact SQL &#41;](../../t-sql/statements/alter-route-transact-sql.md)   
 [CREATE ROUTE (Transact SQL)](../../t-sql/statements/create-route-transact-sql.md)   
 [EVENTDATA (Transact-SQL)](../../t-sql/functions/eventdata-transact-sql.md)   
 [sys.routes &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-routes-transact-sql.md)  
  
  
