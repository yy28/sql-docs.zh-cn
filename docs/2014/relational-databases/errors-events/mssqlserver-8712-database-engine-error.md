---
title: MSSQLSERVER_8712 | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: supportability
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- 8712 (Database Engine error)
ms.assetid: 292fb3bc-062e-41e4-a566-b5d3d0b21977
caps.latest.revision: 12
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: db6b162b08fc60a96bda225b1b2118f5644107d2
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/03/2018
ms.locfileid: "37413756"
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
  
  
