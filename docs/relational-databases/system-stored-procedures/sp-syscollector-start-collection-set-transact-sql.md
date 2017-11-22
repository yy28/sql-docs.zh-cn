---
title: "sp_syscollector_start_collection_set (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syscollector_start_collection_set_TSQL
- sp_syscollector_start_collection_set
dev_langs: TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_start_collection_set
ms.assetid: d8357180-f51e-4681-99f9-0596fe2d2b53
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 32ab8a570febc69a91346e39c8f200a36a263aa8
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="spsyscollectorstartcollectionset-transact-sql"></a>sp_syscollector_start_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  如果已启用收集器但收集组未运行，请启动收集组。 如果未启用收集器，通过运行启用收集器[sp_syscollector_enable_collector](../../relational-databases/system-stored-procedures/sp-syscollector-enable-collector-transact-sql.md)然后使用此存储的过程启动收集组。  

  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_syscollector_start_collection_set   
    [ [ @collection_set_id = ] collection_set_id ]  
    , [[ @name = ] 'name' ]   
```  
  
## <a name="arguments"></a>参数  
 [  **@collection_set_id =** ] *collection_set_id*  
 收集组的唯一本地标识符。 *collection_set_id*是**int**默认值为 NULL。 *collection_set_id*必须具有一个值，如果*名称*为 NULL。  
  
 [  **@name =** ]*名称*  
 是的收集组的名称。 *名称*是**sysname**默认值为 NULL。 *名称*必须具有一个值，如果*collection_set_id*为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 sp_syscollector_create_collection_set 必须在 msdb 系统数据库的上下文中运行，且 SQL Server 代理必须已启用。  
  
 如果对没有计划的收集组运行此过程，则会失败。 如果收集组没有计划 （因为其集合模式已设置为非缓存，例如），请使用[sp_syscollector_run_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-run-collection-set-transact-sql.md)存储过程来启动该收集组。  
  
 此过程将为指定的收集组启用收集和上载作业，并且，如果收集组的 @collection_mode 设置为缓存 (0)，则会立即启动收集代理作业。 有关详细信息，请参阅[sp_syscollector_create_collection_set](../../relational-databases/system-stored-procedures/sp-syscollector-create-collection-set-transact-sql.md)。  
  
 如果收集组不包含任何收集项，则此操作不起作用。 将以警告的形式返回错误 14685。  
  
## <a name="permissions"></a>Permissions  
 若要执行此过程，需具有 dc_operator 固定数据库角色的成员身份。 如果收集组没有代理帐户，则需要具有 sysadmin 固定服务器角色的成员身份。  
  
## <a name="examples"></a>示例  
 下面的示例使用收集组的标识符启动此收集组。  
  
```  
USE msdb;  
GO  
EXEC sp_syscollector_start_collection_set @collection_set_id = 1;  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据收集器存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [数据收集](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets (Transact-SQL)](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
