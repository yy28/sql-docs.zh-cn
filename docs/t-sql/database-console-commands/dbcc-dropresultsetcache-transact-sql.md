---
title: DBCC DROPRESULTSETCACHE (Transact-SQL)
ms.custom: ''
ms.date: 07/03/2019
ms.prod: sql
ms.technology: data-warehouse
ms.reviewer: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 73f598cf-b02a-4dba-8d89-9fc0b55a12b8
author: XiaoyuMSFT
ms.author: xiaoyul
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 35adb2c120eae08cde529b09f8f15f5d45fc29d0
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/20/2020
ms.locfileid: "86484588"
---
# <a name="dbcc-dropresultsetcache--transact-sql"></a>DBCC DROPRESULTSETCACHE (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

从 Azure [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 数据库中删除所有结果集缓存条目。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```syntaxsql
DBCC DROPRESULTSETCACHE
[;]  
```  

## <a name="permissions"></a>权限

要求具有 DB_OWNER 固定服务器角色中的成员资格。

## <a name="remarks"></a>备注

- 此命令将清空所有查询的结果集缓存。  

- 关闭数据库的结果集缓存功能也会删除所有缓存的结果。  

- 暂停启用了结果集缓存的数据库不会删除缓存的结果。  

## <a name="see-also"></a>另请参阅

- [通过结果集缓存进行性能优化](/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
- [ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
- [ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
- [SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
- [DBCC SHOWRESULTCACHESPACEUSED &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-showresultcachespaceused-transact-sql)
