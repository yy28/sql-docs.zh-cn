---
title: MSSQLSERVER_10521 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
helpviewer_keywords:
- 10521 (Database Engine error)
ms.assetid: ba2d7e44-207c-4428-b5f0-c975ac122c0d
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: ecaffb9e40024eca7cbeac77f4b50058e5440cee
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "62870606"
---
# <a name="mssqlserver_10521"></a>MSSQLSERVER_10521
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10521|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_PARAM_NEEDED|  
|消息正文|无法创建计划指南 '%.\*ls'，因为 `@type` 指定为 '%ls'，而参数 '%ls' 为 NULL。 此类型要求该参数的值为非 NULL 值。 请为该参数指定非 NULL 值，或将该类型更改为允许该参数为 NULL 值的类型。|  
  
## <a name="explanation"></a>说明  
 
  `@type` 中指定的类型要求指定参数的值为非 NULL 值；但您指定的是 NULL 值。  
  
## <a name="user-action"></a>用户操作  
 请为该参数指定非 NULL 值，或将该类型更改为允许该参数为 NULL 值的类型。  
  
## <a name="see-also"></a>另请参阅  
 [sp_create_plan_guide &#40;Transact-sql&#41;](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [计划指南](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
