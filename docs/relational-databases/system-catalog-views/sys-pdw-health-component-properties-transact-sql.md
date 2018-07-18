---
title: sys.pdw_health_component_properties (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 66999c0c-dc43-4327-99fb-8366f465e69d
caps.latest.revision: 7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 60e82089b66ff4a8a4263dd56b9ec2871a92869a
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "38058185"
---
# <a name="syspdwhealthcomponentproperties-transact-sql"></a>sys.pdw_health_component_properties (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  描述设备的存储属性。 某些属性显示设备状态和某些属性描述设备本身。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|property_id|**int**|组件的属性的唯一标识符。<br /><br /> property_id 与 component_id 构成此视图的键。|NOT NULL|  
|component_id|**int**|组件的 ID。 请参阅[sys.pdw_health_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。<br /><br /> property_id 与 component_id 构成此视图的键。|NOT NULL|  
|property_name|**nvarchar(255)**|属性的名称。|NOT NULL|  
|physical_name|**nvarchar(32)**|制造商定义的属性名称。|NOT NULL|  
|is_key|**bit**|确定设备实例是唯一的或不是唯一的。|NOT NULL<br /><br /> 0-设备实例是唯一的。<br /><br /> 1-设备实例不是唯一的。|  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
