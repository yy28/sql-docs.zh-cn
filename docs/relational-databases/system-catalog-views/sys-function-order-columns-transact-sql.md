---
title: sys. function_order_columns （Transact-sql） |Microsoft Docs
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
ms.openlocfilehash: a2a51cc56b37325d760ca77f014594496c8ab6b5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68122750"
---
# <a name="sysfunction_order_columns-transact-sql"></a>sys.function_order_columns (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  为每个列返回一行，该列是公共语言运行时（CLR）表值函数的**ORDER**表达式的一部分。  

  
|列名称|数据类型|说明|  
|-----------------|---------------|-----------------|  
|**object_id**|**int**|要定义其顺序的对象（CLR 表值函数）的 ID。|  
|**order_column_id**|**int**|排序列的 ID。 **order_column_id**仅在**object_id**中是唯一的。<br /><br /> **order_column_id**表示此列在排序中的位置。|  
|column_id |**int**|**Object_id**中的列的 ID。<br /><br /> **column_id**仅在**object_id**中是唯一的。|  
|**is_descending**|**bit**|1 = 排序列采用降序排序。<br /><br /> 0 = 排序列采用升序排序。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [&#40;Transact-sql&#41;的对象目录视图](../../relational-databases/system-catalog-views/object-catalog-views-transact-sql.md)   
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)  
  
  
