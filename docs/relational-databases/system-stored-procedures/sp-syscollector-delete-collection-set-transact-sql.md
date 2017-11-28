---
title: "sp_syscollector_delete_collection_set (TRANSACT-SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
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
- sp_syscollector_delete_collection_set_TSQL
- sp_syscollector_delete_collection_set
dev_langs: TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_delete_collecton_set
ms.assetid: 29c63a74-4db4-4068-bd57-9fb519b0c598
caps.latest.revision: "18"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c2f7eeff5b125469add891c39b83151c755b20b5
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="spsyscollectordeletecollectionset-transact-sql"></a>sp_syscollector_delete_collection_set (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  删除用户定义的收集组及其所有收集项。  
  
||  
|-|  
|**适用范围**： [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] （[!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 到 [当前版本](http://go.microsoft.com/fwlink/p/?LinkId=299658)）。|  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法  
  
```  
  
sp_syscollector_delete_collection_set [[ @collection_set_id = ] collection_set_id OUTPUT ]  
    , [[ @name = ] 'name' ]  
```  
  
## <a name="arguments"></a>参数  
 [ @collection_set_id =] *collection_set_id*  
 收集组的唯一标识符。 *collection_set_id*是**int**并且必须具有一个值，如果*名称*为 NULL。  
  
 [ @name =] '*名称*  
 是的收集组的名称。 *名称*是**sysname**并且必须具有一个值，如果*collection_set_id*为 NULL。  
  
## <a name="return-code-values"></a>返回代码值  
 **0** （成功） 或**1** （失败）  
  
## <a name="remarks"></a>注释  
 sp_syscollector_delete_collection_set 必须在 msdb 系统数据库的上下文中运行。  
  
 任一*collection_set_id*或*名称*必须具有一个值，都不能为 NULL。 若要获取这些值，请查询 syscollector_collection_set 系统视图。  
  
 不能删除系统定义的收集组。  
  
## <a name="permissions"></a>Permissions  
 需要具有 dc_admin（拥有 EXECUTE 权限）固定数据库角色的成员身份才能执行此过程。  
  
## <a name="examples"></a>示例  
 以下示例将删除用户定义的收集组指定*collection_set_id*。  
  
```  
USE msdb;  
GO  
EXEC dbo.sp_syscollector_delete_collection_set  
    @collection_set_id = 4;  
```  
  
## <a name="see-also"></a>另请参阅  
 [数据收集器存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [数据收集](../../relational-databases/data-collection/data-collection.md)   
 [syscollector_collection_sets (Transact-SQL)](../../relational-databases/system-catalog-views/syscollector-collection-sets-transact-sql.md)  
  
  
