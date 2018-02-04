---
title: "sys.assembly_types (Transact SQL) |Microsoft 文档"
ms.custom: 
ms.date: 03/15/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.service: 
ms.component: system-catalog-views
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- assembly_types
- sys.assembly_types
- sys.assembly_types_TSQL
- assembly_types_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sys.assembly_types catalog view
ms.assetid: 35f0384f-7a6d-41b1-9461-f1406d68f317
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: f4411b518085338e18b01697fd445ca1d18e7ce1
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2018
---
# <a name="sysassemblytypes-transact-sql"></a>sys.assembly_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  由 CLR 程序集定义的每个用户定义的类型对应一行。 以下**sys.assembly_types**出现在继承列的列表 (请参阅[sys.types &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)) 后**rule_object_id**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|从中创建此类型的程序集的 ID。|  
|**assembly_class**|**sysname**|程序集内定义此类型的类的名称。|  
|**is_binary_ordered**|**bit**|对此类型的字节进行排序等同于对该类型使用比较运算符进行排序。|  
|**is_fixed_length**|**bit**|类型的长度始终与 max_length 相同。|  
|**prog_id**|**nvarchar(40)**|向 COM 公开的类型的 ProgID。|  
|**assembly_qualified_name**|**nvarchar(4000)**|程序集限定类型名。 该名称使用适合传递到 Type.GetType() 的格式。|  
  
## <a name="permissions"></a>权限  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>另请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [标量类型目录视图 &#40;Transact SQL &#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)  
  
  
