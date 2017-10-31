---
title: MSSQLSERVER_10537 | Microsoft Docs
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
- 10537 (Database Engine error)
ms.assetid: 728469a4-6523-4a37-925f-a950d75420fa
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: cguyer
ms.workload: Inactive
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 7b71c60cbafb79dac3f93d9b46ef03040a3b1196
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver10537"></a>MSSQLSERVER_10537
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10537|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_DUP_ENABLED|  
|消息正文|无法启用计划指南 '%.*ls'，因为已启用的计划指南 '%.\*ls' 包含该语句的相同作用域和初始偏移量值。 请先禁用现有计划指南，再启用指定的计划指南。|  
  
## <a name="explanation"></a>解释  
现有计划指南与指定计划指南中的语句包含相同的作用域和初始偏移量值。  
  
## <a name="user-action"></a>用户操作  
请先禁用现有计划指南，再启用指定的计划指南。  
  
## <a name="see-also"></a>另请参阅  
[sp_create_plan_guide (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[计划指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide_from_handle (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  

