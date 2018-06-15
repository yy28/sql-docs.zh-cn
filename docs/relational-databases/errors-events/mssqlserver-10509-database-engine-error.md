---
title: MSSQLSERVER_10509 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
caps.latest.revision: 9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: cf371bbc4a9a80608c5171be9bd9891c71cde1a6
ms.sourcegitcommit: ee661730fb695774b9c483c3dd0a6c314e17ddf8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2018
ms.locfileid: "34321988"
---
# <a name="mssqlserver10509"></a>MSSQLSERVER_10509
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10509|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_INVALID_STMT|  
|消息正文|无法创建计划指南 '%.\*ls'，因为 **@stmt** 或 **@statement_start_offset** 指定的语句包含语法错误或者无法在计划指南中使用。 请提供一个有效的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或者该语句在批中的有效起始位置。 若要获取有效的起始位置，请在 sys.dm_exec_query_stats 动态管理函数中查询 statement_start_offset 列。|  
  
## <a name="explanation"></a>解释  
**@stmt** 或 **@statement_start_offset** 指定的语句包含语法错误或者无法在计划指南中使用。  
  
## <a name="user-action"></a>用户操作  
请提供一个有效的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或者该语句在批中的有效起始位置。 若要获取有效的起始位置，请在 sys.dm_exec_query_stats 动态管理函数中查询 statement_start_offset 列。  
  
## <a name="see-also"></a>另请参阅  
[sp_create_plan_guide (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[计划指南](~/relational-databases/performance/plan-guides.md)  
[sys.dm_exec_query_stats (Transact-SQL)](~/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql.md)  
[sp_create_plan_guide_from_handle (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
