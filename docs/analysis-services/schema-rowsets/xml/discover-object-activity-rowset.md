---
title: "DISCOVER_OBJECT_ACTIVITY 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: schema-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords: DISCOVER_OBJECT_ACTIVITY rowset
ms.assetid: 100f7de1-ad5c-4973-b863-3c10df1245c4
caps.latest.revision: "14"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b3ec98be8fe8e1779364d845a78a8e610734ddab
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="discoverobjectactivity-rowset"></a>DISCOVER_OBJECT_ACTIVITY 行集
  提供在启动服务后每个对象的资源使用情况。  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_OBJECT_ACTIVITY**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**OBJECT_AGGREGATION_HIT**|**是 DBTYPE_I8**||自服务开始后已命中对象聚合的次数。|  
|**OBJECT_AGGREGATION_MISS**|**是 DBTYPE_I8**||自服务开始后尚未丢失（即尚未使用）对象现有聚合的次数。|  
|**OBJECT_CPU_TIME_MS**|**是 DBTYPE_I8**||自服务开始后对象占用的 CPU 时间（毫秒）。|  
|**OBJECT_DATA_VERSION**|**DBTYPE_I4**||对象中数据的沿袭编号；每次处理对象时，此编号随之递增。|  
|**OBJECT_HIT**|**是 DBTYPE_I8**||自服务开始后缓存中已命中对象的次数。|  
|**OBJECT_ID**|**DBTYPE_WSTR**||创建时定义的对象的 ID|  
|**OBJECT_MISS**|**是 DBTYPE_I8**||自服务开始后缓存中已丢失对象的次数。|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**||当前对象的父级的路径。|  
|**OBJECT_READ_KB**|**是 DBTYPE_I8**||自服务开始后对象读取的数据的累计值 (KB)。|  
|**OBJECT_READS**|**是 DBTYPE_I8**||自服务开始后对象的累计读取操作数。|  
|**OBJECT_ROWS_RETURNED**|**是 DBTYPE_I8**||自服务开始后对象返回给调用方的行数。|  
|**OBJECT_ROWS_SCANNED**|**是 DBTYPE_I8**||自服务开始后对象扫描的行数。|  
|**OBJECT_VERSION**|**DBTYPE_I4**||对象的元数据版本号；每次更改对象时，此编号随之发生变化。|  
|**OBJECT_WRITE_KB**|**是 DBTYPE_I8**||自服务开始后对象写入的数据的累计值 (KB)。|  
|**OBJECT_WRITES**|**是 DBTYPE_I8**||自服务开始后对象的累计写入操作数。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_OBJECT_ACTIVTY**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|OBJECT_PARENT_PATH|DBTYPE_WSTR|可选。|  
|OBJECT_ID|DBTYPE_WSTR|可选。|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
