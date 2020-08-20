---
description: sp_syscollector_delete_execution_log_tree (Transact-SQL)
title: sp_syscollector_delete_execution_log_tree (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_delete_execution_log_tree_TSQL
- sp_syscollector_delete_execution_log_tree
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_delete_execution_log_tree
- data collector [SQL Server], stored procedures
ms.assetid: 0a9a7c5b-c3cc-40ca-b524-e948a8cce4e4
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 2b184f469662502613e1340e3642cab153597b8c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88463989"
---
# <a name="sp_syscollector_delete_execution_log_tree-transact-sql"></a>sp_syscollector_delete_execution_log_tree (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  删除与单个收集组的运行有关的所有日志项。 这还将从此运行的 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 表中删除日志项。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_syscollector_delete_execution_log_tree[ @log_id = ] log_id  
          , [ @from_collection_set = ] from_collection_set  
```  
  
## <a name="arguments"></a>参数  
`[ @log_id = ] log_id` 收集组日志的唯一标识符。 *log_id* 是 **int**。  
  
`[ @from_collection_set = ] from_collection_set` 收集组的标识符。 *from_collection_set* 是 **bit = 1**。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或 **1** (失败)   
  
## <a name="permissions"></a>权限  
 需要具有 EXECUTE 权限的 **dc_operator** (中的成员身份) 固定数据库角色才能执行此过程。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
