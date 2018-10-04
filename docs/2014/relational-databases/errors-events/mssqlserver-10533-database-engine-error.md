---
title: MSSQLSERVER_10533 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10533 (Database Engine error)
ms.assetid: cc2fbdab-7b90-415f-a1f9-066824344283
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 86bd82dfd095baeacb35f8454859adb938123f52
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48066337"
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
  
## <a name="see-also"></a>请参阅  
 [计划指南](../performance/plan-guides.md)   
 [sp_create_plan_guide (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
