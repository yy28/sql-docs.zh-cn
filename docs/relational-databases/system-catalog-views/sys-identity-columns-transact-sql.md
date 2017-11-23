---
title: "sys.identity_columns (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- identity_columns
- sys.identity_columns
- sys.identity_columns_TSQL
- identity_columns_TSQL
dev_langs: TSQL
helpviewer_keywords: sys.identity_columns catalog view
ms.assetid: 97ee01e6-9c9e-4fd9-884b-68b4084669d5
caps.latest.revision: "44"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 2669f1373bedec1256d3071b9fe1f85b7c8dab8f
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/21/2017
---
# <a name="sysidentitycolumns-transact-sql"></a>sys.identity_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-all-md](../../includes/tsql-appliesto-ss2008-all-md.md)]

  作为标识列的每个列各占一行。  
  
 **Sys.identity_columns**视图继承中的行**sys.columns**视图。 **Sys.identity_columns**视图返回中的列**sys.columns**视图中，加上**seed_value**， **increment_value**， **last_value**，和**is_not_for_replication**列。 有关详细信息，请参阅[目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**\<列继承自 sys.columns >**||**Sys.identity_columns**视图返回中的所有列**sys.columns**视图。 它还返回如下所述的其他列。 有关列的说明， **sys.identity_columns**视图继承自**sys.columns**，请参阅[sys.columns &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-columns-transact-sql.md).|  
|**seed_value**|**sql_variant**|该标识列的种子值。 种子值的数据类型与列本身的数据类型相同。|  
|**increment_value**|**sql_variant**|该标识列的增量值。 种子值的数据类型与列本身的数据类型相同。|  
|**last_value**|**sql_variant**|为该标识列生成的最后一个值。 种子值的数据类型与列本身的数据类型相同。|  
|**is_not_for_replication**|**bit**|标识列声明为 NOT FOR REPLICATION。|  
  
> [!NOTE]  
>  要创建一个可在多个表中使用的自动递增数字或者可以从应用程序中调用而不引用任何表的自动递增数字，请参阅[序列号](../../relational-databases/sequence-numbers/sequence-numbers.md)。  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [对象目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [查询 SQL Server 系统目录常见问题解答](../../relational-databases/system-catalog-views/querying-the-sql-server-system-catalog-faq.md)  
  
  
