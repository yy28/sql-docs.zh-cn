---
title: DISCOVER_OBJECT_ACTIVITY 行集 |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: schema-rowsets
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: ae63c9ebff71e124b5843873db380af3d2e6e660
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34030278"
---
# <a name="discoverobjectactivity-rowset"></a>DISCOVER_OBJECT_ACTIVITY 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  提供在启动服务后每个对象的资源使用情况。  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_OBJECT_ACTIVITY**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**OBJECT_AGGREGATION_HIT**|**DBTYPE_I8**||自服务开始后已命中对象聚合的次数。|  
|**OBJECT_AGGREGATION_MISS**|**DBTYPE_I8**||自服务开始后尚未丢失（即尚未使用）对象现有聚合的次数。|  
|**OBJECT_CPU_TIME_MS**|**DBTYPE_I8**||自服务开始后对象占用的 CPU 时间（毫秒）。|  
|**OBJECT_DATA_VERSION**|**DBTYPE_I4**||对象中数据的沿袭编号；每次处理对象时，此编号随之递增。|  
|**OBJECT_HIT**|**DBTYPE_I8**||自服务开始后缓存中已命中对象的次数。|  
|**OBJECT_ID**|**DBTYPE_WSTR**||创建时定义的对象的 ID|  
|**OBJECT_MISS**|**DBTYPE_I8**||自服务开始后缓存中已丢失对象的次数。|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**||当前对象的父级的路径。|  
|**OBJECT_READ_KB**|**DBTYPE_I8**||自服务开始后对象读取的数据的累计值 (KB)。|  
|**OBJECT_READS**|**DBTYPE_I8**||自服务开始后对象的累计读取操作数。|  
|**OBJECT_ROWS_RETURNED**|**DBTYPE_I8**||自服务开始后对象返回给调用方的行数。|  
|**OBJECT_ROWS_SCANNED**|**DBTYPE_I8**||自服务开始后对象扫描的行数。|  
|**OBJECT_VERSION**|**DBTYPE_I4**||对象的元数据版本号；每次更改对象时，此编号随之发生变化。|  
|**OBJECT_WRITE_KB**|**DBTYPE_I8**||自服务开始后对象写入的数据的累计值 (KB)。|  
|**OBJECT_WRITES**|**DBTYPE_I8**||自服务开始后对象的累计写入操作数。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_OBJECT_ACTIVTY**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|OBJECT_PARENT_PATH|DBTYPE_WSTR|選擇性。|  
|OBJECT_ID|DBTYPE_WSTR|選擇性。|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
