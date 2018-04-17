---
title: sys.registered_search_property_lists (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- registered_search_property_lists_TSQL
- sys.registered_search_property_lists
- registered_search_property_lists
- sys.registered_search_property_lists_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- full-text search [SQL Server], search property lists
- sys.registered_search_property_lists catalog view
- search property lists [SQL Server], viewing
ms.assetid: 630d4caa-9bea-4cd3-a5b1-01098b0855fc
caps.latest.revision: 16
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a3581b5af74c6b9d23157e3806c68bfbd0db1854
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="sysregisteredsearchpropertylists-transact-sql"></a>sys.registered_search_property_lists (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  当前数据库中的每个搜索属性列表各占一行。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**property_list_id**|**int**|属性列表的 ID。|  
|**名称**|**sysname**|属性列表的名称。|  
|**create_date**|**datetime**|属性列表的创建日期。|  
|**modify_date**|**datetime**|上次使用任意 ALTER 语句修改属性列表的日期。|  
|**principal_id**|**int**|属性列表的所有者。|  
  
## <a name="remarks"></a>注释  
 有关详细信息，请参阅 [使用搜索属性列表搜索文档属性](../../relational-databases/search/search-document-properties-with-search-property-lists.md)。  
  
## <a name="permissions"></a>权限  
 搜索属性列表的元数据可见性仅限于您拥有或已向您授予部分 REFERENCE 权限的搜索属性列表。  
  
> [!NOTE]  
>  搜索属性列表所有者可以授予列表的 REFERENCE 或 CONTROL 权限。 具有 CONTROL 权限的用户还可以向其他用户授予 REFERENCE 权限。  
  
## <a name="examples"></a>示例  
 以下示例显示 [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)] 数据库中的搜索属性列表的 ID 和名称。  
  
```  
USE AdventureWorks2012;  
GO  
SELECT property_list_id, name FROM sys.registered_search_property_lists;  
GO  
```  
  
## <a name="see-also"></a>另请参阅  
 [ALTER FULLTEXT INDEX (Transact-SQL)](../../t-sql/statements/alter-fulltext-index-transact-sql.md)   
 [sys.fulltext_indexes (Transact-SQL)](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)  
  
  
