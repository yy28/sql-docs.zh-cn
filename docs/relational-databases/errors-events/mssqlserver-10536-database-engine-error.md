---
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b00f374672490cf9823a3c7700d4ae0e53e18c3f
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver10536"></a>MSSQLSERVER_10536
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10536|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_TOO_MANY_STMTS|  
|消息正文|无法创建计划指南 '%.\*ls'，因为与指定的 **@plan_handle** 对应的批处理或模块中包含的合格语句超过 1000 个。 通过为每个语句指定 **statement_start_offset** 值，为批处理或模块中的每个语句创建一个计划指南。|  
  
## <a name="explanation"></a>解释  
与指定的 **@plan_handle** 对应的批处理或模块中包含的合格语句超过 1000 个。  
  
## <a name="user-action"></a>用户操作  
通过为每个语句指定 **statement_start_offset** 值，为批处理或模块中的每个语句创建一个计划指南。  
  
## <a name="see-also"></a>另请参阅  
[sp_create_plan_guide (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[计划指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

