---
title: MSSQLSERVER_10536 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 10536 (Database Engine error)
ms.assetid: 9f97b41f-0ef8-4ad2-aec0-906a5d7522ba
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: ffa9509c55632c5f041f060c499be0a8bc7cbf4b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015462"
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
|消息正文|无法创建计划指南 ' %。\*ls 因为批处理或模块对应于指定`@plan_handle`包含超过 1000 个符合条件的语句。 通过为每个语句指定 `statement_start_offset` 值，为批或模块中的每个语句创建一个计划指南。|  
  
## <a name="explanation"></a>解释  
 与指定的 `@plan_handle` 对应的批或模块中包含的合格语句超过 1000 个。  
  
## <a name="user-action"></a>用户操作  
 通过为每个语句指定 `statement_start_offset` 值，为批或模块中的每个语句创建一个计划指南。  
  
## <a name="see-also"></a>请参阅  
 [sp_create_plan_guide (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [计划指南](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
