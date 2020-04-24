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
ms.openlocfilehash: f6821ae2ee11a6cd8e5713996cc04b3330a63300
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "81632323"
---
# <a name="dbcc-showresultcachespaceused-transact-sql"></a>DBCC SHOWRESULTCACHESPACEUSED (Transact-SQL)

[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-xxxxxx-xxxx-asdw-xxx-md.md)]

显示 Azure [!INCLUDE[ssSDW](../../includes/sssdw-md.md)] 数据库的结果集缓存所用的存储空间。
  
![主题链接图标](../../database-engine/configure-windows/media/topic-link.gif "“主题链接”图标") [Transact-SQL 语法约定 (Transact-SQL)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>语法  
  
```syntaxsql
DBCC SHOWRESULTCACHESPACEUSED  
[;]  
```  
## <a name="remarks"></a>备注

`DBCC SHOWRESULTCACHESPACEUSED` 命令不使用任何参数，并且会返回运行此命令的数据库所使用的空间。

## <a name="permissions"></a>权限

需要 VIEW SERVER STATE 权限。
  
## <a name="result-sets"></a>结果集  
  
|列|数据类型|说明|  
|------------|---------------|-----------------|  
|reserved_space|bigint|用于数据库的总空间，单位为 KB。 该数字在缓存的结果集增加时会改变。|  
|data_space|bigint|用于数据的空间，单位为 KB。|  
|index_space|bigint|用于索引的空间，单位为 KB。|  
|unused_space|bigint|保留空间中未使用的空间，单位为 KB。|  


## <a name="see-also"></a>另请参阅

[通过结果集缓存进行性能优化](/azure/sql-data-warehouse/performance-tuning-result-set-caching)</br>
[ALTER DATABASE SET 选项 (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql-set-options?view=azure-sqldw-latest)</br>
[ALTER DATABASE (Transact-SQL)](/sql/t-sql/statements/alter-database-transact-sql?view=azure-sqldw-latest)</br>
[SET RESULT SET CACHING &#40;Transact-SQL&#41;](/sql/t-sql/statements/set-result-set-caching-transact-sql)</br>
[DBCC DROPRESULTSETCACHE &#40;Transact-SQL&#41;](/sql/t-sql/database-console-commands/dbcc-dropresultsetcache-transact-sql)
