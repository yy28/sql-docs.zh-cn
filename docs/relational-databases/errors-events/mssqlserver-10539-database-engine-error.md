---
title: MSSQLSERVER_10539 | Microsoft Docs
ms.custom: ''
ms.date: 04/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 10539 (Database Engine error)
ms.assetid: 49c26ff7-18b8-4f07-a087-f45f63463b3b
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8334c28865c01c63ae6bcb18c79d4fd88b715175
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68060602"
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
  
