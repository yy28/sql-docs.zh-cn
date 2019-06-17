---
title: sys.function_order_columns (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- function_order_columns
- sys.function_order_columns_TSQL
- function_order_columns_TSQL
- sys.function_order_columns
dev_langs:
- TSQL
helpviewer_keywords:
- sys.function_order_columns catalog view
ms.assetid: 29287973-3125-4d35-8ca9-92cb45828854
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 43ce8d82bc286e7005d57d5a829e09814ffdd240
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63004734"
---
# <a name="sysfunctionordercolumns-transact-sql"></a>sys.function_order_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  每一部分的列返回一行**顺序**该列语言运行时 (CLR) 表值函数的表达式。  

  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|要定义其顺序的对象（CLR 表值函数）的 ID。|  
|**order_column_id**|**int**|排序列的 ID。 **order_column_id**仅中是唯一**object_id**。<br /><br /> **order_column_id**表示此列在排序中的位置。|  
|**column_id**|**int**|中列的 ID **object_id**。<br /><br /> **column_id**仅中是唯一**object_id**。|  
|**is_descending**|**bit**|1 = 排序列采用降序排序。<br /><br /> 0 = 排序列采用升序排序。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [对象目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
