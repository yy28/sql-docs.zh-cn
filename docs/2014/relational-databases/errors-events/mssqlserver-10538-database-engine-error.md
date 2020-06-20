---
title: MSSQLSERVER_10538 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10538 (Database Engine error)
ms.assetid: 284d19b4-4979-4cbe-a9be-ac1104433c69
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: edc6abf192a3341f9b84c99e99071343cc882c3d
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2020
ms.locfileid: "84968107"
---
# <a name="mssqlserver_10538"></a>MSSQLSERVER_10538
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10538|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_INVALID_PLANGUIDE_HANDLE|  
|消息正文|因为指定的计划指南 ID 为 NULL 或无效，或者您对该计划指南引用的对象没有所需权限，所以找不到该计划指南。 请确保计划指南 ID 有效，当前会话设置为正确的数据库上下文，并且你对计划指南所引用的对象具有 ALTER DATABASE 权限或 ALTER 权限。|  
  
## <a name="explanation"></a>说明  
 指定的计划指南 ID 为 NULL 或无效，或者您对该计划指南引用的对象没有所需权限。  
  
## <a name="user-action"></a>用户操作  
 请确保计划指南 ID 有效，当前会话设置为正确的数据库上下文，并且你对计划指南所引用的对象具有 ALTER DATABASE 权限或 ALTER 权限。  
  
## <a name="see-also"></a>另请参阅  
 [sp_create_plan_guide (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [计划指南](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
