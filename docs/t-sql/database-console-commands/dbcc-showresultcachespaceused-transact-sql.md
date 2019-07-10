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
author: XiaoyuL-Preview
ms.author: xiaoyul
manager: craigg
monikerRange: = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 9a6d45a5307c98add48d35feab3db2dfb981fa4b
ms.sourcegitcommit: e4b241fd92689c2aa6e1f5e625874bd0b807dd01
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/04/2019
ms.locfileid: "67566539"
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
  
## <a name="see-also"></a>另请参阅

[ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
[DBCC DROPRESULTSETCACHE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)