---
title: sys.periods (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 25e66ed3-2270-4c5c-9f5a-2c0f165a57ca
caps.latest.revision: 6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca6eea06d877ec9a6a92c35d0bd01401300f3974
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
ms.locfileid: "33180103"
---
# <a name="sysperiods-transact-sql"></a>sys.periods (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-ss2016-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-xxxx-xxxx-xxx-md.md)]

  返回为其定义期间每个表的行。  
  
|列标题|数据类型|Description|  
|-------------------|---------------|-----------------|  
|period_type|**sysname**|期间的名称|  
|period_type_desc|**tinyint**|表示的期间的类型的数字值：<br /><br /> 1 = 系统时间段|  
|object_id|**nvarchar(60)**|列的类型的文本说明：<br /><br /> SYSTEM_TIME_PERIOD|  
|object_id|**int**|包含 period_type 列的表的 id|  
|start_column_id|**int**|定义的较低的时间段边界列的 id|  
|end_column_id|**int**|定义时间段上限列的 id|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [系统视图&#40;Transact SQL&#41;](http://msdn.microsoft.com/library/35a6161d-7f43-4e00-bcd3-3091f2015e90)   
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [sys.all_columns &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-all-columns-transact-sql.md)   
 [sys.system_columns &#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/sys-system-columns-transact-sql.md)   
 [查询的 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)   
 [临时表](../../relational-databases/tables/temporal-tables.md)  
  
  
