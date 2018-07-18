---
title: MSSQLSERVER_10509 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 10509 (Database Engine error)
ms.assetid: e9dd5357-ee3d-420a-9a89-d12ab5404e73
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: a0f66b064e6239f3bad07587520744e5529ab777
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37415926"
---
# <a name="mssqlserver10509"></a>MSSQLSERVER_10509
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10509|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_INVALID_STMT|  
|消息正文|无法创建计划指南 ' %。\*ls' 指定的语句由于`@stmt`或`@statement_start_offset`包含语法错误或者无法在计划指南中使用。 请提供一个有效的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或者该语句在批中的有效起始位置。 若要获取有效的起始位置，请在 sys.dm_exec_query_stats 动态管理函数中查询 statement_start_offset 列。|  
  
## <a name="explanation"></a>解释  
 `@stmt` 或 `@statement_start_offset` 指定的语句包含语法错误或者无法在计划指南中使用。  
  
## <a name="user-action"></a>用户操作  
 请提供一个有效的 [!INCLUDE[tsql](../../includes/tsql-md.md)] 语句或者该语句在批中的有效起始位置。 若要获取有效的起始位置，请在 sys.dm_exec_query_stats 动态管理函数中查询 statement_start_offset 列。  
  
## <a name="see-also"></a>请参阅  
 [sp_create_plan_guide (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [计划指南](../performance/plan-guides.md)   
 [sys.dm_exec_query_stats &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/sys-dm-exec-query-stats-transact-sql)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
