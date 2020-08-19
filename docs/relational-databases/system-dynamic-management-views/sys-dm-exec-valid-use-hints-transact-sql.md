---
description: 'sys. dm_exec_valid_use_hints (Transact-sql) '
title: sys. dm_exec_valid_use_hints (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 11/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
f1_keywords:
- sys.dm_exec_valid_use_hints
- sys.dm_exec_valid_use_hints_TSQL
- dm_exec_valid_use_hints
- dm_exec_valid_use_hints_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_valid_use_hints management view
ms.assetid: 65d50589-39c2-4046-92b6-0c4587d8c593
author: pmasl
ms.author: pelopes
ms.openlocfilehash: f05b4e01f06c354d461b1455e499c83a13d2d76c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88489898"
---
# <a name="sysdm_exec_valid_use_hints-transact-sql"></a>sys. dm_exec_valid_use_hints (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

返回 [使用提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint) 支持的提示名称。 每行列出一个提示名称。  
  
使用此 DMV 查看使用提示表示法下所有支持的提示的列表。  
  
|列名|数据类型|说明|  
|-----------------|---------------|-----------------|  
|name|**sysname**|提示的名称。|

有关每个提示的说明，请参阅 [查询提示](../../t-sql/queries/hints-transact-sql-query.md#use_hint) 。

SP1 中引入的 [!INCLUDE[ssSQL15_md](../../includes/sssql15-md.md)] 。
  
## <a name="see-also"></a>另请参阅  
    
 [动态管理视图和函数 (Transact-SQL)](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [与数据库相关的动态管理视图 &#40;Transact-sql&#41;](../../relational-databases/system-dynamic-management-views/database-related-dynamic-management-views-transact-sql.md)  

