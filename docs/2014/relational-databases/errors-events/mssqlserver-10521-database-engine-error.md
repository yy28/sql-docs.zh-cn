---
title: MSSQLSERVER_10521 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 10521 (Database Engine error)
ms.assetid: ba2d7e44-207c-4428-b5f0-c975ac122c0d
caps.latest.revision: 10
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 18d823ff21a38c3eeee8df725c9a38172080d40e
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37421076"
---
# <a name="mssqlserver10521"></a>MSSQLSERVER_10521
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10521|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_PARAM_NEEDED|  
|消息正文|无法创建计划指南 ' %。\*ls' 因为`@type`指定了 '%ls' 为 '%ls' 和参数为 NULL。 此类型要求该参数的值为非 NULL 值。 请为该参数指定非 NULL 值，或将该类型更改为允许该参数为 NULL 值的类型。|  
  
## <a name="explanation"></a>解释  
 `@type` 中指定的类型要求指定参数的值为非 NULL 值；但您指定的是 NULL 值。  
  
## <a name="user-action"></a>用户操作  
 请为该参数指定非 NULL 值，或将该类型更改为允许该参数为 NULL 值的类型。  
  
## <a name="see-also"></a>请参阅  
 [sp_create_plan_guide (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [计划指南](../performance/plan-guides.md)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
