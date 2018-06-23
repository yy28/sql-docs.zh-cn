---
title: MSSQLSERVER_10519 | Microsoft Docs
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
- 10519 (Database Engine error)
ms.assetid: 3be393a1-b186-41ae-afb9-a3d07ff354bb
caps.latest.revision: 10
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: fa8bb26aeb39ca6b46f29063664a15ec43a86cc1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36027905"
---
# <a name="mssqlserver10519"></a>MSSQLSERVER_10519
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10519|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_INCOMPATIBLE_STMT_AND_HINTS|  
|消息正文|无法创建计划指南 ' %。\*ls 中指定提示因为`@hints`不能应用于通过以下任一方式指定的语句`@stmt`或`@statement_start_offset`。 请确保提示可以应用于该语句。|  
  
## <a name="explanation"></a>解释  
 `@hints` 中指定的语句无法应用于 `@stmt` 或 `@statement_start_offset` 指定的语句。  
  
## <a name="user-action"></a>用户操作  
 请指定可以应用于该语句的提示。  
  
## <a name="see-also"></a>请参阅  
 [sp_create_plan_guide (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [计划指南](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
