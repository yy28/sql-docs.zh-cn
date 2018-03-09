---
title: "sys.sp_xtp_merge_checkpoint_files (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 11/28/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sys.sp_xtp_merge_checkpoint_files_TSQL
- sys.sp_xtp_merge_checkpoint_files
dev_langs:
- TSQL
helpviewer_keywords:
- sys.sp_xtp_merge_checkpoint_files
ms.assetid: da04df2a-f7a1-41e7-a1ef-2d5d68919892
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f2ea57de40e24824a71d4d89ad954fb19fe21e29
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysspxtpmergecheckpointfiles-transact-sql"></a>sys.sp_xtp_merge_checkpoint_files (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  **sys.sp_xtp_merge_checkpoint_files**合并指定的事务范围中的所有数据和差异文件。  
  
 有关详细信息，请参阅[创建和管理用于内存优化对象的存储](../../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)。  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
||  
|-|  
|**请注意**： 此存储的过程中已弃用[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。 它不再需要并不能使用，启动[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]。|  
  
## <a name="syntax"></a>语法  
  
```  
  
sys.sp_xtp_merge_checkpoint_files database_name, @transaction_lower_bound, @transaction_upper_bound  
[;]  
```  
  
## <a name="arguments"></a>参数  
 *database_name*  
 数据库的名称，将对该数据库调用合并。 如果数据库没有内存中表，则此过程将返回用户错误。 如果数据库处于离线状态，则它恢复错误。  
  
 *lower_bound_Tid*  
 为数据文件中所示的事务 (bigint) 下限[sys.dm_db_xtp_checkpoint_files &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md)对应于启动检查点文件的合并。 对于无效的 transactonId 值将生成错误。  
  
 *upper_bound_Tid*  
 为数据文件中所示的事务 (bigint) 上限[sys.dm_db_xtp_checkpoint_files &#40;Transact SQL &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql.md). 对于无效的 transactonId 值将生成错误。  
  
## <a name="return-code-values"></a>返回代码值  
 InclusionThresholdSetting  
  
## <a name="cursors-returned"></a>返回的游标  
 InclusionThresholdSetting  
  
## <a name="permissions"></a>权限  
 需要 sysadmin 固定服务器角色和 db_owner 固定数据库角色。  
  
## <a name="remarks"></a>注释  
 将有效范围内的所有数据和差异文件合并，以生成单个数据文件和差异文件。 此过程不支持合并策略。  
  
## <a name="see-also"></a>另请参阅  
 [系统存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [内存中 OLTP（内存中优化）](../../relational-databases/in-memory-oltp/in-memory-oltp-in-memory-optimization.md)  
  
  
