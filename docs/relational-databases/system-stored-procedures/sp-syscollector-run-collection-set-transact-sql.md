---
description: sp_syscollector_run_collection_set (Transact-SQL)
title: sp_syscollector_run_collection_set (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_run_collection_set_TSQL
- sp_syscollector_run_collection_set
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_run_collection_set
- data collector [SQL Server], stored procedures
ms.assetid: 7bbaee48-dfc7-45c0-b11f-c636b6a7e720
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 69ba3790a9b1805eb4d717ad23fa284494ce14af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481017"
---
# <a name="sp_syscollector_run_collection_set-transact-sql"></a>sp_syscollector_run_collection_set (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  如果已启用收集器并将收集组配置为非缓存收集模式，则启动收集组。  
  
> [!NOTE]  
>  如果针对配置为缓存收集模式的收集组运行此过程，则会失败。  
  
 利用 sp_syscollector_run_collection_set，用户能够根据需要创建数据快照。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_syscollector_run_collection_set [[ @collection_set_id = ] collection_set_id ]  
          , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>参数  
`[ @collection_set_id = ] collection_set_id` 收集组的唯一本地标识符。 *collection_set_id* 为 **int** ，并且 *name* 为 NULL 时必须具有值。  
  
`[ @name = ] 'name'` 收集组的名称。 *名称* 为 **sysname** ，并且 *collection_set_id* 为 NULL 时必须具有值。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** (成功) 或 **1** (失败)   
  
## <a name="remarks"></a>备注  
 *Collection_set_id*或*name*必须具有值，两者都不能为 NULL。  
  
 此过程将为指定的收集组启动收集和上载作业，如果收集组的** \@ collection_mode**设置为非缓存 (1) ，则会立即启动收集代理作业。 有关详细信息，请参阅 [&#40;transact-sql&#41;sp_syscollector_create_collection_set ](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)。  
  
 sp_sycollector_run_collection_set 还可用于运行没有计划的收集组。  
  
## <a name="permissions"></a>权限  
 需要具有 EXECUTE 权限的 **dc_operator** (中的成员身份) 固定数据库角色才能执行此过程。  
  
## <a name="example"></a>示例  
 使用收集组的标识符启动收集组。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_run_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;系统存储过程 ](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [“数据收集”](../../relational-databases/data-collection/data-collection.md)  
  
  
