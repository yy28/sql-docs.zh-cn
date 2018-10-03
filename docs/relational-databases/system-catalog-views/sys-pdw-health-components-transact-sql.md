---
title: sys.pdw_health_components (TRANSACT-SQL) |Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: pdw
ms.reviewer: ''
ms.technology: system-objects
ms.topic: conceptual
ms.assetid: d5c7589b-09b0-4f12-ab84-feb3ec3fbaaa
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d8f0032eab0067f845ecc4f67a7b009d0ee1b676
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47731067"
---
# <a name="syspdwhealthcomponents-transact-sql"></a>sys.pdw_health_components (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  存储有关所有组件和系统中存在的设备信息。 其中包括硬件、 存储设备和网络设备。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|component_id|**int**|组件或设备的唯一标识符。<br /><br /> 此视图的键。|NOT NULL|  
|group_id|**Int**|此组件所属的逻辑组件组。 请参阅[sys.pdw_health_components （并行数据仓库）](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。|NOT NULL|  
|component_name|**nvarchar(255)**|组件的名称。|NOT NULL|  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
