---
title: sys.sp_cleanup_temporal_history |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: ''
ms.prod_service: sql-database
ms.service: sql-database
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 6eff30b4-b261-4f1f-b93c-1f69d754298d
caps.latest.revision: 4
author: CarlRabeler
ms.author: carlrab
manager: craigg
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: 6216ca6584c2bf6d78bb66096145cd49428398dc
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38051192"
---
# <a name="sysspcleanuptemporalhistory-transact-sql"></a>sys.sp_cleanup_temporal_history (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-xxxxxx-asdb-xxxx-xxx-md.md)]

 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  

匹配单个事务中的配置的 HISTORY_RETENTION 期的时态历史记录表中删除所有行。
  
## <a name="syntax"></a>语法  
```  
sp_cleanup_temporal_history [@schema_name = ] schema_name, [@table_name = ] table_name [, [@row_count=] @row_count_var [OUTPUT]]
```  
  
## <a name="arguments"></a>参数  

*@table_name*

清理调用的保留期的时态表的名称。

*schema_name*

当前临时表所属的架构的名称

*row_count_var* [OUTPUT]

输出参数返回的已删除的行数。 如果历史记录表具有聚集列存储索引，将返回此参数始终为 0。
  
## <a name="remarks"></a>Remarks
此存储的过程可用于仅临时表，具有有限保留期指定。
仅当你需要立即清除历史记录表中的所有过期的行时，才使用此存储的过程。 您应该知道，它会有重大影响的数据库日志和 I/O 子系统上，删除在同一事务中所有符合条件的行。 

建议始终依赖于清理内部后台任务删除过期的行上的常规工作负载和在常规的数据库的影响降到最低。

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
