---
title: MSSQLSERVER_8712 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
caps.latest.revision: 12
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 09ad71165e148069fdb07dc42b27f24015a07b52
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36123404"
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
  
## <a name="see-also"></a>请参阅  
 [查询提示 (Transact-SQL)](/sql/t-sql/queries/hints-transact-sql-query)   
 [计划指南](../performance/plan-guides.md)  
  
  
