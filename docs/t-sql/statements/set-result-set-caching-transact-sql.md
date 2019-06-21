---
title: SET RESULT_SET_CACHING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 05/03/2019
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 561e92512ded10b06926f5b23f0f5d40540e3d2d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66826872"
---
# <a name="set-result-set-caching-transact-sql-applies-to-azure-sql-data-warehouse-gen2-only-preview"></a>SET RESULT SET CACHING (Transact-SQL) 仅适用于 Azure SQL 数据仓库 Gen2（预览版）

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

让 Azure SQL 数据仓库缓存查询结果集。
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [TRANSACT-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法

```
SET RESULT_SET_CACHING { ON | OFF };
```  
  
## <a name="remarks"></a>Remarks  

> [!Note]
> 虽然此功能正在推广到所有区域，但请检查部署到实例的版本以及最新的 [Azure SQL DW 发行说明](/azure/sql-data-warehouse/release-notes-10-0-10106-0)以了解功能可用性。
  
连接到 master 数据库时，必须运行此命令。  对此数据库设置的更改立即生效。  缓存查询结果集会产生存储成本。 在你为数据库禁用结果缓存后，以前保留的结果缓存会立即从 Azure SQL 数据仓库存储中删除。 [sys.databases](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql?view=azure-sqldw-latest) 中引入了新列 is_result_set_caching_on，用于显示数据库的结果缓存设置。  

ON  指定在 Azure SQL 数据仓库存储中缓存从此数据库返回的查询结果集。

OFF  指定不在 Azure SQL 数据仓库存储中缓存从此数据库返回的查询结果集。

用户可以使用特定的 request_id 来查询 [sys.pdw_request_steps](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql?view=azure-sqldw-latest)，从而判断查询是否已执行且结果集是缓存命中还是缓存失误。 如果结果集是缓存命中，查询结果包含一个具有以下详细信息的步骤：

|**列名**|**“运算符”**|**ReplTest1**|
|----|----|----|
|operation_type|=|ReturnOperation|
|step_index|=|0|
|location_type|=|Control|
|command|Like|%DWResultCacheDb%|
||||
  
## <a name="permissions"></a>权限

需要以下权限：

- 服务器级别主体登录名（由预配进程创建）；或
- dbmanager 数据库角色的成员。

数据库所有者无法更改数据库，除非所有者是 dbmanager 角色的成员。
  
## <a name="examples"></a>示例

### <a name="enable-result-set-caching-for-a-database"></a>为数据库启用结果集缓存

```sql
ALTER DATABASE myTestDW  
SET RESULT_SET_CACHING ON;
```

### <a name="disable-result-set-caching-for-a-database"></a>为数据库禁用结果集缓存

```sql
ALTER DATABASE myTestDW  
SET RESULT_SET_CACHING OFF;
```

### <a name="check-result-set-caching-setting-for-a-database"></a>检查数据库的结果集缓存设置

```sql
SELECT name, is_result_set_caching_on  
FROM sys.databases
```

### <a name="check-for-number-of-queries-with-result-set-cache-hit-and-cache-miss"></a>检查结果集是缓存命中和缓存失误的查询数

```sql
SELECT  
Queries=CacheHits+CacheMisses,
CacheHits,
CacheMisses,
CacheHitPct=CacheHits*1.0/(CacheHits+CacheMisses)
FROM  
(SELECT  
CacheHits=count(distinct case when s.command like '%DWResultCacheDb%' and
r.resource_class IS NULL and s.operation_type = 'ReturnOperation' and  
s.step_index = 0 then s.request_id else null end) ,
CacheMisses=count(distinct case when r.resource_class IS NOT NULL then  
s.request_id else null end)
     FROM sys.dm_pdw_request_steps s  
     JOIN sys.dm_pdw_exec_requests r  
     ON s.request_id = r.request_id) A
```

### <a name="check-for-result-set-cache-hit-or-cache-miss-for-a-query"></a>检查查询的结果集是缓存命中还是缓存失误

```sql
If
(SELECT step_index  
FROM sys.dm_pdw_request_steps  
WHERE request_id = 'QID58286'
      and operation_type = 'ReturnOperation'
      and command like '%DWResultCacheDb%') = 0
SELECT 1 as is_cache_hit  
ELSE
SELECT 0 as is_cache_hit
```

### <a name="check-for-all-queries-with-result-set-cache-hits"></a>检查结果集是缓存命中的所有查询

```sql
SELECT *  
FROM sys.dm_pdw_request_steps  
WHERE command like '%DWResultCacheDb%' and step_index = 0
```

## <a name="see-also"></a>另请参阅

[SET 语句 (Transact-SQL)](../../t-sql/statements/set-statements-transact-sql.md)</br>
[ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)