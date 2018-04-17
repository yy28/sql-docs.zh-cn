---
title: sys.pdw_health_alerts (Transact SQL) |Microsoft 文档
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: pdw
ms.service: ''
ms.component: system-catalog-views
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 49c01e5f-ee47-41a0-871d-35a759f50851
caps.latest.revision: 7
author: barbkess
ms.author: barbkess
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 7647cc1fdc4182c8423e0eca4de429736e4acee9
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/16/2018
---
# <a name="syspdwhealthalerts-transact-sql"></a>sys.pdw_health_alerts (TRANSACT-SQL)
[!INCLUDE[tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md](../../includes/tsql-appliesto-xxxxxx-xxxx-xxxx-pdw-md.md)]

  不同的警报会在系统; 上的存储属性这是警报的目录表。  
  
|列名|数据类型|Description|范围|  
|-----------------|---------------|-----------------|-----------|  
|alert_id|**int**|警报的唯一标识符。<br /><br /> 此视图的键。|NOT NULL|  
|component_id|**int**|此警报适用于组件的 ID。 组件是一个常规组件标识符，例如"提供的电源，"，并不是特定于安装。 请参阅[sys.pdw_health_components &#40;TRANSACT-SQL&#41;](../../relational-databases/system-catalog-views/sys-pdw-health-components-transact-sql.md)。|NOT NULL|  
|alert_name|**nvarchar(255)**|警报名称。|NOT NULL|  
|state|**nvarchar(32)**|警报状态。|NOT NULL<br /><br /> 可能的值：<br /><br /> 操作<br /><br /> 不再运行<br /><br /> 已降级<br /><br /> 已失败|  
|severity|**nvarchar(32)**|警报的严重性。|NOT NULL<br /><br /> 可能的值：<br /><br /> 信息性<br /><br /> 警告<br /><br /> 错误|  
|type|**nvarchar(32)**|类型的警报。|NOT NULL<br /><br /> 可能的值：<br /><br /> StatusChange-设备状态已更改。<br /><br /> 阈值的值超出阈值的值。|  
|description|**nvarchar(4000)**|警报描述。|NOT NULL|  
|条件 (condition)|**nvarchar(255)**|键入时使用 = 阈值。 定义如何计算警报阈值。|NULL|  
|status|**nvarchar(32)**|警报状态|NULL|  
|condition_value|**bit**|指示是否允许警报系统操作过程中发生。|NULL<br /><br /> 可能值<br /><br /> 0-不会生成警报。<br /><br /> 1-将生成警报。|  
  
## <a name="see-also"></a>另请参阅  
 [SQL 数据仓库和并行数据仓库目录视图](../../relational-databases/system-catalog-views/sql-data-warehouse-and-parallel-data-warehouse-catalog-views.md)  
  
  
