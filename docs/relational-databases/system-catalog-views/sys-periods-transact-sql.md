---
description: 'sys.databases (Transact-sql) '
title: sys.databases (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 25e66ed3-2270-4c5c-9f5a-2c0f165a57ca
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 8c2aecc1b4547812a4e388297270761481956835
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/08/2020
ms.locfileid: "89546685"
---
# <a name="sysperiods-transact-sql"></a>sys.databases (Transact-sql) 
[!INCLUDE [sqlserver2016](../../includes/applies-to-version/sqlserver2016.md)]

  为已为其定义了期间的每个表返回一行。  
  
|列标题|数据类型|说明|  
|-------------------|---------------|-----------------|  
|name|**sysname**|期间名称|  
|period_type|**tinyint**|表示期间类型的数值：<br /><br /> 1 = 系统时间段|  
|period_type_desc|**nvarchar(60)**|列类型的文本说明：<br /><br /> SYSTEM_TIME_PERIOD|  
|object_id|**int**|包含 period_type 列的表的 id|  
|start_column_id|**int**|定义下端句号边界的列的 id|  
|end_column_id|**int**|定义上 period 边界的列的 id|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [Transact-sql&#41;的系统视图 &#40;](https://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys. all_columns &#40;Transact-sql&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [ &#40;Transact-sql 的 tem_columnssys.sys&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [临时表](../../relational-databases/tables/temporal-tables.md)  
  
  
