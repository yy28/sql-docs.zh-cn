---
title: sys. pdw_health_component_properties （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 2b31baacea8d4754fbc81e1c1c747a2c95b1402b
ms.sourcegitcommit: 1be90e93980a8e92275b5cc072b12b9e68a3bb9a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/09/2020
ms.locfileid: "84627056"
---
# <a name="syspdw_health_component_properties-transact-sql"></a>sys. pdw_health_component_properties （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  存储用于描述设备的属性。 某些属性显示设备状态，一些属性描述设备本身。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|组件的属性的唯一标识符。<br /><br /> property_id 和 component_id 构成此视图的键。|NOT NULL|  
|component_id|**int**|组件的 ID。 请参阅[sys.databases &#40;transact-sql&#41;pdw_health_components ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。<br /><br /> property_id 和 component_id 构成此视图的键。|NOT NULL|  
|property_name|**nvarchar(255)**|属性的名称。|NOT NULL|  
|physical_name|**nvarchar(32)**|制造商定义的属性名称。|NOT NULL|  
|is_key|**bit**|确定设备实例是否唯一。|NOT NULL<br /><br /> 0-设备实例是唯一的。<br /><br /> 1-设备实例不唯一。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
