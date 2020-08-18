---
description: 'sys. pdw_health_components (Transact-sql) '
title: sys. pdw_health_components (Transact-sql) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: d5c7589b-09b0-4f12-ab84-feb3ec3fbaaa
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 74b741d94d5e9a10c4b657cfbe70ad69f9cbbfa1
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88400763"
---
# <a name="syspdw_health_components-transact-sql"></a>sys. pdw_health_components (Transact-sql) 
[!INCLUDE [pdw](../../includes/applies-to-version/pdw.md)]

  存储有关系统中存在的所有组件和设备的信息。 其中包括硬件、存储设备和网络设备。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|组件或设备的唯一标识符。<br /><br /> 此视图的键。|NOT NULL|  
|group_id|**Int**|此组件所属的逻辑组件组。 请参阅 [ (并行数据仓库) 的 pdw_health_components ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。|NOT NULL|  
|component_name|**nvarchar(255)**|组件的名称。|NOT NULL|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
