---
title: syscollector_collection_items (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- syscollector_collection_items_TSQL
- syscollector_collection_items
dev_langs:
- TSQL
helpviewer_keywords:
- syscollector_collection_items view
- add data collector view
ms.assetid: a279ecd1-a59c-4315-9f08-bf221f00a465
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 53f978bf7914776e8596a89b0ee9b62770cd6866
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62760220"
---
# <a name="syscollectorcollectionitems-transact-sql"></a>syscollector_collection_items (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  返回有关收集组中的项的信息。  
  
|列名|数据类型|Description|  
|-----------------|---------------|-----------------|  
|**collection_set_id**|**int**|标识收集组。 不可为 null。|  
|**collection_item_id**|**int**|标识收集组中的项。 不可为 null。|  
|**collector_type_uid**|**uniqueidentifier**|用于标识收集器类型的 GUID。 不可为 null。|  
|**名称**|**nvarchar(4000)**|收集组的名称。 可以为 Null。|  
|**frequency**|**int**|收集项收集数据的频率。 不可为 null。|  
|**参数**|**xml**|介绍与相应收集项关联的收集器类型的参数化。 此收集项的 XML 架构验证与 XML 架构 (XSD) 存储在**parameter_schema**特定收集器类型。 可以为 Null。 有关详细信息，请参阅[syscollector_collector_types &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/syscollector-collector-types-transact-sql.md)。|  
  
## <a name="permissions"></a>权限  
 需要为选择**dc_operator**， **dc_proxy**。  
  
## <a name="see-also"></a>请参阅  
 [数据收集器存储过程 (Transact-SQL)](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [数据收集器视图 (Transact-SQL)](../../relational-databases/system-catalog-views/data-collector-views-transact-sql.md)   
 [“数据收集”](../../relational-databases/data-collection/data-collection.md)  
  
  
