---
title: MSSQLSERVER_8689 | Microsoft Docs
ms.custom: 
ms.date: 04/04/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
helpviewer_keywords:
- 8689 (Database Engine error)
ms.assetid: 99467a32-6576-4272-a076-b16c06933f2a
caps.latest.revision: 14
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e6de76f8ef1fe370e8dc1361631b6776440ea172
ms.contentlocale: zh-cn
ms.lasthandoff: 06/22/2017

---
# <a name="mssqlserver8689"></a>MSSQLSERVER_8689
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|8689|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|USEPLAN_ERR_NO_DB|  
|消息正文|USE PLAN 提示中指定的数据库 '%.*ls' 不存在。 请指定一个现有数据库。|  
  
## <a name="explanation"></a>解释  
USE PLAN 提示中指定的数据库不存在。  
  
## <a name="user-action"></a>用户操作  
请确保在 USE PLAN 提示中指定的所有数据库均存在。  
  
## <a name="see-also"></a>另请参阅  
[查询提示 (Transact-SQL)](~/t-sql/queries/hints-transact-sql-query.md)  
[计划指南](~/relational-databases/performance/plan-guides.md)  
  

