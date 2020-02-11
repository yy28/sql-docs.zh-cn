---
title: sys. pdw_health_alerts （Transact-sql） |Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.technology: system-objects
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
author: ronortloff
ms.author: rortloff
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: c47bcc342bf8a052aed93649ca0ad8475d937608
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2020
ms.locfileid: "68127542"
---
# <a name="syspdw_health_alerts-transact-sql"></a>sys. pdw_health_alerts （Transact-sql）
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  存储系统上可能发生的不同警报的属性;这是一个用于警报的目录表。  
  
|列名|数据类型|说明|范围|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|警报的唯一标识符。<br /><br /> 此视图的键。|NOT NULL|  
|component_id|**int**|应用此警报的组件的 ID。 组件是一般组件标识符（如 "电源"），并且不特定于安装。 请参阅[sys.databases &#40;transact-sql&#41;pdw_health_components ](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。|NOT NULL|  
|alert_name|**nvarchar(255)**|警报的名称。|NOT NULL|  
|state|**nvarchar （32）**|警报的状态。|NOT NULL<br /><br /> 可能的值：<br /><br /> 营业<br /><br /> 'NonOperational'<br /><br /> 降级<br /><br /> 因|  
|severity|**nvarchar （32）**|警报的严重性。|NOT NULL<br /><br /> 可能的值：<br /><br /> 条<br /><br /> 出现<br /><br /> 条|  
|type|**nvarchar （32）**|警报的类型。|NOT NULL<br /><br /> 可能的值：<br /><br /> StatusChange-设备状态已更改。<br /><br /> 阈值-值超出了阈值。|  
|description|**nvarchar(4000)**|警报的说明。|NOT NULL|  
|条件|**nvarchar(255)**|Type = 阈值时使用。 定义如何计算警报阈值。|Null|  
|status|**nvarchar （32）**|警报状态|Null|  
|condition_value|**bit**|指示是否允许在系统操作过程中出现警报。|Null<br /><br /> 可能的值<br /><br /> 0-不生成警报。<br /><br /> 1-生成警报。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
