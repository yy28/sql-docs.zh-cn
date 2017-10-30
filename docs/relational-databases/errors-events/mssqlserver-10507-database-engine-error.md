---
title: MSSQLSERVER_10507 | Microsoft Docs
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
- 10507 (Database Engine error)
ms.assetid: cd83fa81-ac37-4eda-a3c3-17610b051de2
caps.latest.revision: 9
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 0943ae13586a5ceefe2a6ec7e07b7cb498a1b525
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver10507"></a>MSSQLSERVER_10507
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10507|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_STMT_DOES_NOT_MATCH|  
|消息正文|无法创建计划指南 '%.\*ls'，因为 **@stmt** 和 **@module_or_batch** 或 **@plan_handle** 和 **@statement_start_offset** 指定的语句与指定模块或批处理中的所有语句都不匹配。 请修改这些值以匹配模块或批中的语句。|  
  
## <a name="explanation"></a>解释  
指定模块或批中的语句无法与指定的语句或语句偏移量值相匹配。  
  
## <a name="user-action"></a>用户操作  
请修改指定的参数值，使其与模块或批中的语句相匹配。  
  
## <a name="see-also"></a>另请参阅  
[计划指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

