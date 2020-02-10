---
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e5ddb4df0089b488d3a15c76a76abef8be154848
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62870520"
---
# <a name="mssqlserver_10536"></a>MSSQLSERVER_10536
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10536|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_TOO_MANY_STMTS|  
|消息正文|无法创建计划指南 '%.\*ls'，因为与指定的 `@plan_handle` 对应的批处理或模块中包含的合格语句超过 1000 个。 通过为每个语句指定 `statement_start_offset` 值，为批或模块中的每个语句创建一个计划指南。|  
  
## <a name="explanation"></a>说明  
 与指定的 `@plan_handle` 对应的批或模块中包含的合格语句超过 1000 个。  
  
## <a name="user-action"></a>用户操作  
 通过为每个语句指定 `statement_start_offset` 值，为批或模块中的每个语句创建一个计划指南。  
  
## <a name="see-also"></a>另请参阅  
 [sp_create_plan_guide &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [计划指南](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
