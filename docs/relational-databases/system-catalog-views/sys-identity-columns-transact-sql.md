---
title: sys. identity_columns （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- identity_columns
- sys.identity_columns
- sys.identity_columns_TSQL
- identity_columns_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.identity_columns catalog view
ms.assetid: 97ee01e6-9c9e-4fd9-884b-68b4084669d5
author: VanMSFT
ms.author: vanto
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 49684671c25ea83fa7554bec7f80d0b16c30d4eb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68122719"
---
# <a name="sysidentity_columns-transact-sql"></a>sys.identity_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  作为标识列的每个列各占一行。  
  
 **Sys.databases identity_columns**视图继承**sys.databases**视图中的行。 **Sys. identity_columns**视图返回**sys.databases**视图中的列，以及**seed_value**、 **increment_value**、 **last_value**和**is_not_for_replication**列。 有关详细信息，请参阅[目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)。  
  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**\<从 sys.databases 继承的列>**||**Sys. identity_columns**视图返回**sys.databases**视图中的所有列。 它还返回如下所述的其他列。 有关**sys.databases identity_columns**视图继承自**sys.databases**的列的说明，请参阅[&#40;transact-sql&#41;的 sys.databases。 ](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md)|  
|**seed_value**|**sql_variant**|该标识列的种子值。 种子值的数据类型与列本身的数据类型相同。|  
|**increment_value**|**sql_variant**|该标识列的增量值。 种子值的数据类型与列本身的数据类型相同。|  
|**last_value**|**sql_variant**|为该标识列生成的最后一个值。 种子值的数据类型与列本身的数据类型相同。|  
|**is_not_for_replication**|**bit**|标识列声明为 NOT FOR REPLICATION。|  
  
> [!NOTE]  
>  要创建一个可在多个表中使用的自动递增数字或者可以从应用程序中调用而不引用任何表的自动递增数字，请参阅[序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;的对象目录视图](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
