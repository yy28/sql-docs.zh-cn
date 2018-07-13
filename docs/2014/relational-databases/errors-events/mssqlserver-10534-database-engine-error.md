---
title: MSSQLSERVER_10534 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 10534 (Database Engine error)
ms.assetid: e65bb118-99d5-4fdb-b1d5-0ec70f0a677b
caps.latest.revision: 15
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 9814659977492d93b5d2ae330a948d0622eda442
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413496"
---
# <a name="mssqlserver10534"></a>MSSQLSERVER_10534
    
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|10534|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|PG_INVALID_PARAMS|  
|消息正文|无法创建计划指南 ' %。\*ls' 指定的值由于`@params`无效。 请以 *parameter_name parameter_type* 的形式指定该值，或指定 NULL。|  
  
## <a name="explanation"></a>解释  
 为 `@params` 指定的值无效。  
  
## <a name="user-action"></a>用户操作  
 请以 *parameter_name parameter_type* 的形式指定该值，或指定 NULL。  
  
## <a name="see-also"></a>请参阅  
 [计划指南](../performance/plan-guides.md)   
 [sp_create_plan_guide (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-transact-sql)   
 [sp_create_plan_guide_from_handle (Transact-SQL)](/sql/relational-databases/system-stored-procedures/sp-create-plan-guide-from-handle-transact-sql)  
  
  
