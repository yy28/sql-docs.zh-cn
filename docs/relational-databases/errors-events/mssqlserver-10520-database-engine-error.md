---
title: MSSQLSERVER_10520 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: errors-events
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords: 10520 (Database Engine error)
ms.assetid: cc8799f1-5b90-4248-b209-e1d5087f9529
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 92ec45949632fb9c820da5979c5b119105662fdc
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="mssqlserver10520"></a>MSSQLSERVER_10520
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10520|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_PARAM_NOT_ALLOWED|  
|消息正文|无法创建计划指南 '%.*ls'，因为 @type 指定为 '%ls' ，并且为参数 '%ls' 指定了非 NULL 值。 此类型要求该参数的值为 NULL 值。 请为该参数指定 NULL 值，或将该类型更改为允许该参数为非 NULL 值的类型。|  
  
## <a name="explanation"></a>解释  
@type 中指定的类型要求指定参数的值为 NULL 值，但却提供了非 NULL 值。  
  
## <a name="user-action"></a>用户操作  
请为该参数指定 NULL 值，或将该类型更改为允许该参数为非 NULL 值的类型。  
  
## <a name="see-also"></a>另请参阅  
[sp_create_plan_guide (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[计划指南](~/relational-databases/performance/plan-guides.md)  
  
