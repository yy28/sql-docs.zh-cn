---
title: sys.sp_cleanup_temporal_history |Microsoft 文档
ms.custom: ''
ms.date: 03/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.service: sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 6eff30b4-b261-4f1f-b93c-1f69d754298d
caps.latest.revision: 4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.workload: Inactive
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: f86d01146c3861f599e85e7bb7c61f716a3bf4b8
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="sysspcleanuptemporalhistory-transact-sql"></a>sys.sp_cleanup_temporal_history (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

从匹配配置的 HISTORY_RETENTION 时间段，在单个事务中的临时历史记录表中删除所有行。
  
## <a name="syntax"></a>语法  
```  
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```  
  
## <a name="arguments"></a>参数  

*@table_name*

有关哪些保持调用清理临时表的名称。

*schema_name*

当前临时表所属的架构名称

*row_count_var* [OUTPUT]

输出参数返回的已删除的行数。 如果历史记录表具有聚集列存储索引，此参数将返回始终为 0。
  
## <a name="remarks"></a>注释
此存储的过程可以在具有有限指定保持期只能与临时表使用。
仅当你需要立即清除历史记录表中的所有过期的行，请使用此存储的过程。 您应该知道，它会有重大影响的数据库日志和 I/O 子系统，它删除同一事务中的所有符合条件的行。 

建议始终依赖于清理内部后台任务删除过期的常规工作负载和一般的数据库上的最小影响的行。

## <a name="permissions"></a>权限  
 需要 db_owner 权限。  

## <a name="example"></a>示例

```
declare @rowcnt int
EXEC sys.sp_cleanup_temporal_history 'dbo', 'Department', @rowcnt output
select @rowcnt
```

## <a name="see-also"></a>另请参阅

[临时表保留策略](https://docs.microsoft.com/azure/sql-database/sql-database-temporal-tables-retention-policy)
