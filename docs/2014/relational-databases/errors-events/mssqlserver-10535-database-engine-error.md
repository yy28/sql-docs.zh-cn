---
title: MSSQLSERVER_10535 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 10535 (Database Engine error)
ms.assetid: 478fd978-11d9-4155-8329-f599fdbec14b
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ff4797fdd9d206ca459bc84facccfc588aafba00
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126860"
---
# <a name="mssqlserver10535"></a>MSSQLSERVER_10535
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10535|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_NO_PLAN|  
|消息正文|由于在计划缓存中找不到与指定计划句柄对应的计划，因此无法创建计划指南 '%.*ls'。 请指定已缓存的计划句柄。 有关已缓存的计划句柄的列表，请查询 sys.dm_exec_query_stats 动态管理视图。|  
  
## <a name="explanation"></a>解释  
 未在与指定的计划句柄相对应的计划缓存中找到计划。  
  
## <a name="user-action"></a>用户操作  
 请指定已缓存的计划句柄。 有关已缓存的计划句柄的列表，请查询 sys.dm_exec_query_stats 动态管理视图。  
  
## <a name="see-also"></a>请参阅  
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)   
 [sys.dm_exec_query_stats (Transact-SQL)](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)  
  
  
