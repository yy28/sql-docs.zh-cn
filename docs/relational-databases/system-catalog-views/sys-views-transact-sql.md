---
title: sys.views (Transact SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- views_TSQL
- views
- sys.views_TSQL
- sys.views
dev_langs:
- TSQL
helpviewer_keywords:
- sys.views catalog view
ms.assetid: f8a8ea39-5a09-4662-801e-b43519467def
author: stevestein
ms.author: sstein
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: f5f7d4c9c6bb44d978007170abfff5a7730b028a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68095532"
---
# <a name="sysviews-transact-sql"></a>sys.views (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  与每个视图对象，一行**sys.objects.type** = V。  
  
|列名|数据类型|描述|  
|-----------------|---------------|-----------------|  
|**\<继承列 >**||此视图所继承的列的列表，请参阅[sys.objects &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-objects-transact-sql.md)|  
|**is_replicated**|**bit**|1 = 视图已复制。|  
|**has_replication_filter**|**bit**|1 = 视图具有复制筛选器。|  
|**has_opaque_metadata**|**bit**|1 = 为视图指定了 VIEW_METADATA 选项。 有关详细信息，请参阅 [CREATE VIEW (Transact-SQL)](../../t-sql/statements/create-view-transact-sql.md)。|  
|**has_unchecked_assembly_data**|**bit**|1 = 视图包含依赖于一个程序集的持久化数据，该程序集在上次使用 ALTER ASSEMBLY 期间更改了定义。 在下一次成功执行 DBCC CHECKDB 或 DBCC CHECKTABLE 后重置为 0。|  
|**with_check_option**|**bit**|1 = 在视图定义中指定了 WITH CHECK OPTION。|  
|**is_date_correlation_view**|**bit**|1 = 系统自动创建视图，以存储 datetime 列之间的依赖关系信息。 通过将 DATE_CORRELATION_OPTIMIZATION 设置为 ON，启用创建此视图。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [ALTER ASSEMBLY (Transact-SQL)](../../t-sql/statements/alter-assembly-transact-sql.md)   
 [DBCC CHECKDB (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md)   
 [DBCC CHECKTABLE (Transact-SQL)](../../t-sql/database-console-commands/dbcc-checktable-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题解答](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
