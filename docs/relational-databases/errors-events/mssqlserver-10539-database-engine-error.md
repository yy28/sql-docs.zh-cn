---
title: MSSQLSERVER_10539 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: errors-events
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
caps.latest.revision: 9
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: dcfff7f43261bb24da3eec97753f52e1ea0839b1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="mssqlserver10539"></a>MSSQLSERVER_10539
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10539|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_NO_PLAN_FOR_STMT|  
|消息正文|由于查询计划对于初始偏移量为 %d 的语句不可用，因此无法从缓存创建计划指南 '%.*ls'。 如果该语句依赖于尚未创建的数据库对象，则可能出现此问题。 请确保所有必要的数据库对象都已存在，并在创建该计划指南之前先执行该语句。|  
  
## <a name="explanation"></a>解释  
在计划缓存中，查询计划不能用于具有指定初始偏移量的语句。  
  
## <a name="user-action"></a>用户操作  
请确保所有必要的数据库对象都已存在，并在创建该计划指南之前先执行该语句。  
  
## <a name="see-also"></a>另请参阅  
[sp_create_plan_guide_from_handle (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
