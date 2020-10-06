---
description: SET RESULT_SET_CACHING (Transact-SQL)
title: SET RESULT_SET_CACHING (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/16/2020
ms.prod: sql
ms.prod_service: sql-data-warehouse
ms.reviewer: jrasnick
ms.technology: t-sql
ms.topic: language-reference
f1_keywords: ''
dev_langs:
- TSQL
helpviewer_keywords: ''
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: =azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: f8247062993b33a669477be7d71363efa45ead32
ms.sourcegitcommit: 2f868a77903c1f1c4cecf4ea1c181deee12d5b15
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2020
ms.locfileid: "91670540"
---
# <a name="set-result-set-caching-transact-sql"></a>SET RESULT_SET_CACHING (Transact-SQL) 

[!INCLUDE [asa](../../includes/applies-to-version/asa.md)]

控制当前客户端会话的结果集缓存行为。  

适用于 [!INCLUDE[ssSDW](../../includes/sssdwfull-md.md)]  
  
 ![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>语法

```syntaxsql
SET RESULT_SET_CACHING { ON | OFF };
```  

[!INCLUDE[synapse-analytics-od-unsupported-syntax](../../includes/synapse-analytics-od-unsupported-syntax.md)]

## <a name="remarks"></a>备注  

连接到要为其配置 result_set_caching 设置的用户数据库时，请运行此命令。

**ON**   
启用当前客户端会话的结果集缓存。  如果已在数据库级别将结果集缓存设置为“OFF”，就无法为会话将它设置为“ON”。

**OFF**   
禁用当前客户端会话的结果集缓存。

## <a name="examples"></a>示例

使用查询的 request_id 查询 [sys.dm_pdw_exec_requests](/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql) 中的 result_cache_hit 列以查看是否使用结果缓存命中或未命中执行此查询。

```sql
SELECT result_cache_hit
FROM sys.dm_pdw_exec_requests
WHERE request_id = 'QID58286'
```

## <a name="permissions"></a>权限

要求具有公共角色的成员身份

## <a name="see-also"></a>另请参阅

- [通过结果集缓存进行性能优化](/azure/sql-data-warehouse/performance-tuning-result-set-caching)
- [ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest&preserve-view=true)
- [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest&preserve-view=true)
- [DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-showresultcachespaceused-transact-sql)
- [DBCC DROPRESULTSETCACHE (Transact-SQL)](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)
