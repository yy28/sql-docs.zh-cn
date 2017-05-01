---
title: MSSQLSERVER_8712 | Microsoft Docs
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
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
caps.latest.revision: 12
author: BYHAM
ms.author: rickbyh
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 65489fa755c5dda3459d7de227631591f821e5bd
ms.lasthandoff: 04/11/2017

---
# <a name="mssqlserver8712"></a>MSSQLSERVER_8712
  
## <a name="details"></a>详细信息  
  
|||  
|-|-|  
|产品名称|SQL Server|  
|事件 ID|8712|  
|事件源|MSSQLSERVER|  
|组件|SQLEngine|  
|符号名称|USEPLAN_ERR_NO_INDEX|  
|消息正文|USE PLAN 提示中指定的索引 '%.*ls' 不存在。 请指定一个现有索引，或者使用指定名称创建一个索引。|  
  
## <a name="explanation"></a>解释  
USE PLAN 提示中指定的索引不存在。  
  
## <a name="user-action"></a>用户操作  
请确保在 USE PLAN 提示中指定的所有索引均存在。  
  
## <a name="see-also"></a>另请参阅  
[查询提示 (Transact-SQL)](~/t-sql/queries/hints-transact-sql-query.md)  
[计划指南](~/relational-databases/performance/plan-guides.md)  
  

