---
title: MSSQLSERVER_10531 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10531 (Database Engine error)
ms.assetid: bb40e994-231c-44ce-933f-8d767fb2f450
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 8de08a9760b1df4d3c8be4d57009e0bcb2d71b6e
ms.sourcegitcommit: b57d98e9b2444348f95c83a24b8eea0e6c9da58d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2020
ms.locfileid: "86554152"
---
# <a name="mssqlserver_10531"></a>MSSQLSERVER_10531
    
## <a name="details"></a>详细信息  
  
|Attribute|值|  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10531|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_NO_ELIGIBLE_STMT|  
|消息正文|因为用户没有足够的权限，所以无法从缓存创建计划指南 '%.*ls'。 请为创建该计划指南的用户授予 VIEW SERVER STATE 权限。|  
  
## <a name="explanation"></a>说明  
 用户权限不足，无法从计划缓存创建指定的计划指南。  
  
## <a name="user-action"></a>用户操作  
 请为创建该计划指南的用户授予 VIEW SERVER STATE 权限。  
  
## <a name="see-also"></a>另请参阅  
 [计划指南](../performance/plan-guides.md)   
 [sp_create_plan_guide (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
