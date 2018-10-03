---
title: sys.assembly_types (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: system-objects
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
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: '>=aps-pdw-2016||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 1f62185fc99512a966789f1b878b23f90264fba9
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47721267"
---
# <a name="sysassemblytypes-transact-sql"></a>sys.assembly_types (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-pdw-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-pdw-md.md)]

  由 CLR 程序集定义的每个用户定义的类型对应一行。 以下**sys.assembly_types**继承的列列表中显示 (请参阅[sys.types &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-types-transact-sql.md)) 后**rule_object_id**。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**assembly_id**|**int**|从中创建此类型的程序集的 ID。|  
|**assembly_class**|**sysname**|程序集内定义此类型的类的名称。|  
|**is_binary_ordered**|**bit**|对此类型的字节进行排序等同于对该类型使用比较运算符进行排序。|  
|**is_fixed_length**|**bit**|类型的长度始终与 max_length 相同。|  
|**prog_id**|**nvarchar(40)**|向 COM 公开的类型的 ProgID。|  
|**assembly_qualified_name**|**nvarchar(4000)**|程序集限定类型名。 该名称使用适合传递到 Type.GetType() 的格式。|  
  
## <a name="permissions"></a>Permissions  
 [!INCLUDE[ssCatViewPerm](../../includes/sscatviewperm-md.md)] 有关详细信息，请参阅 [Metadata Visibility Configuration](../../relational-databases/security/metadata-visibility-configuration.md)。  
  
## <a name="see-also"></a>请参阅  
 [目录视图 (Transact-SQL)](../../relational-databases/system-catalog-views/catalog-views-transact-sql.md)   
 [标量类型目录视图&#40;Transact SQL&#41;](../../relational-databases/system-catalog-views/scalar-types-catalog-views-transact-sql.md)  
  
  
