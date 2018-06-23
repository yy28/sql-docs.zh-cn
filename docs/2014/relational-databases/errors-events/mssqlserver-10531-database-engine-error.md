---
title: MSSQLSERVER_10531 | Microsoft Docs
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
- 10531 (Database Engine error)
ms.assetid: bb40e994-231c-44ce-933f-8d767fb2f450
caps.latest.revision: 9
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 7e1c38822b6386d011723c15cdd7a58c48c65029
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138863"
---
# <a name="mssqlserver10531"></a>MSSQLSERVER_10531
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10531|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_NO_ELIGIBLE_STMT|  
|消息正文|因为用户没有足够的权限，所以无法从缓存创建计划指南 '%.*ls'。 请为创建该计划指南的用户授予 VIEW SERVER STATE 权限。|  
  
## <a name="explanation"></a>解释  
 用户权限不足，无法从计划缓存创建指定的计划指南。  
  
## <a name="user-action"></a>用户操作  
 请为创建该计划指南的用户授予 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>请参阅  
 [计划指南](../performance/plan-guides.md)   
 [sp_create_plan_guide (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
