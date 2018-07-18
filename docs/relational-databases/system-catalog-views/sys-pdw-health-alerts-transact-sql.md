---
title: sys.pdw_health_alerts (TRANSACT-SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: pdw
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
caps.latest.revision: 7
author: ronortloff
ms.author: rortloff
manager: craigg
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 6f8281d520f64580af8432dbf2004227ce628d41
ms.sourcegitcommit: e77197ec6935e15e2260a7a44587e8054745d5c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2018
ms.locfileid: "37987189"
---
# <a name="syspdwhealthalerts-transact-sql"></a>sys.pdw_health_alerts (Transact SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  不同的警报系统; 上可能出现的存储属性这是警报目录表。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|警报的唯一标识符。<br /><br /> 此视图的键。|NOT NULL|  
|component_id|**int**|此警报适用于组件的 ID。 组件是一个常规组件标识符，例如"提供的电源，"，并不特定于安装。 请参阅[sys.pdw_health_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。|NOT NULL|  
|alert_name|**nvarchar(255)**|警报的名称。|NOT NULL|  
|state|**nvarchar(32)**|警报的状态。|NOT NULL<br /><br /> 可能的值：<br /><br /> 操作<br /><br /> 不再运行<br /><br /> 已降级<br /><br /> 失败|  
|severity|**nvarchar(32)**|警报的严重性。|NOT NULL<br /><br /> 可能的值：<br /><br /> 通知<br /><br /> 警告<br /><br /> 错误|  
|type|**nvarchar(32)**|警报的类型。|NOT NULL<br /><br /> 可能的值：<br /><br /> StatusChange-设备状态已更改。<br /><br /> 阈值-在值超过阈值的值。|  
|description|**nvarchar(4000)**|警报的描述。|NOT NULL|  
|条件 (condition)|**nvarchar(255)**|键入时使用 = 阈值。 定义如何计算警报的阈值。|NULL|  
|status|**nvarchar(32)**|警报状态|NULL|  
|condition_value|**bit**|指示是否允许该警报在系统操作期间发生。|NULL<br /><br /> 可能值<br /><br /> 0-不生成警报。<br /><br /> 1-将生成警报。|  
  
## <a name="see-also"></a>请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
