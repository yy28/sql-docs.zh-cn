---
title: MSSQLSERVER_10534 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10534 (Database Engine error)
ms.assetid: e65bb118-99d5-4fdb-b1d5-0ec70f0a677b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 4f718b124bb9fa0fba37619349d2efc0a3bb643f
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060666"
---
# <a name="mssqlserver10534"></a>MSSQLSERVER_10534
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10534|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_INVALID_PARAMS|  
|消息正文|无法创建计划指南 '%.\*ls'，因为为 **@params** 指定的值无效。 请以 *parameter_name parameter_type* 的形式指定该值，或指定 NULL。|  
  
## <a name="explanation"></a>解释  
为 **@params** 指定的值无效。  
  
## <a name="user-action"></a>用户操作  
请以 *parameter_name parameter_type* 的形式指定该值，或指定 NULL。  
  
## <a name="see-also"></a>另请参阅  
[计划指南](~/relational-databases/performance/plan-guides.md)  
[sp_create_plan_guide (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql.md)  
[sp_create_plan_guide_from_handle (Transact-SQL)](~/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql.md)  
  
