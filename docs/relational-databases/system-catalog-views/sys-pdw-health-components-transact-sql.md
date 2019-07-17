---
title: sys.pdw_health_components (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: d5c7589b-09b0-4f12-ab84-feb3ec3fbaaa
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 5205c1ac6248f5aadee01410b4ba5e8f00332a73
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68127487"
---
# <a name="syspdwhealthcomponents-transact-sql"></a>sys.pdw_health_components (Transact-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  存储有关所有组件和系统中存在的设备信息。 其中包括硬件、 存储设备和网络设备。  
  
|列名|数据类型|描述|范围|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|组件或设备的唯一标识符。<br /><br /> 此视图的键。|NOT NULL|  
|group_id|**Int**|此组件所属的逻辑组件组。 请参阅[sys.pdw_health_components （并行数据仓库）](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。|NOT NULL|  
|component_name|**nvarchar(255)**|组件的名称。|NOT NULL|  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
