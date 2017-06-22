---
title: MSSQLSERVER_10533 | Microsoft Docs
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
- 10533 (Database Engine error)
ms.assetid: cc2fbdab-7b90-415f-a1f9-066824344283
caps.latest.revision: 10
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: caf664dd00f9e7261c1a688f1c3c710ea96679be
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver10533"></a>MSSQLSERVER_10533
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10533|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_NAME_TOO_BIG|  
|消息正文|无法创建计划指南 '%.*ls'，因为其名称超过允许的最大字符数 124。 请指定字符数少于 125 个的名称。|  
  
## <a name="explanation"></a>解释  
计划指南的名称超过所允许的最大字符数（即 124 个字符）。  
  
## <a name="user-action"></a>用户操作  
请指定字符数少于 125 个的名称。  
  
## <a name="see-also"></a>另请参阅  
[计划指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

