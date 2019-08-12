---
title: DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL) | Microsoft Docs
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
ms.openlocfilehash: ffd0ad4ddcdae91071811e57cdb8c5f6aaaea656
ms.sourcegitcommit: db9bed6214f9dca82dccb4ccd4a2417c62e4f1bd
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/24/2019
ms.locfileid: "68476308"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

显示 Azure [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 数据库的结果集缓存所用的存储空间。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "主题链接图标") [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```sql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  
## <a name="remarks"></a>Remarks

`DBCC SHOWRESULTCACHESPACEUSED` 命令不使用任何参数，并且会返回运行此命令的数据库所使用的空间。

每个数据集的结果集缓存的最大大小为 1 TB。  在以下情况下，Azure SQL 数据仓库将自动逐出结果集缓存中的项：

- 尚未使用结果集（每 48 小时执行一次）。
- 结果集缓存达到最大大小。

用户可以关闭结果集缓存功能或使用 `DBCC DROPRESULTSETCACHE` 命令，来手动清空数据库的结果集缓存。   暂停数据库无法将结果集缓存清空。  

## <a name="permissions"></a>权限

需要 VIEW SERVER STATE 权限。
  
## <a name="result-sets"></a>结果集  
  
|“列”|数据类型|描述|  
|------------|---------------|-----------------|  
|reserved_space|BIGINT|用于数据库的总空间，单位为 KB。 该数字在缓存的结果集增加时会改变。|  
|data_space|BIGINT|用于数据的空间，单位为 KB。|  
|index_space|BIGINT|用于索引的空间，单位为 KB。|  
|unused_space|BIGINT|保留空间中未使用的空间，单位为 KB。|  


## <a name="see-also"></a>另请参阅

[ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
[DBCC DROPRESULTSETCACHE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)