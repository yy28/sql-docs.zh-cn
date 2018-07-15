---
title: DISCOVER_OBJECT_ACTIVITY 行集 |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- DISCOVER_OBJECT_ACTIVITY rowset
ms.assetid: 100f7de1-ad5c-4973-b863-3c10df1245c4
caps.latest.revision: 14
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 09aec1da2c7e9001585b0793b12f0faf89feaf27
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37235697"
---
# <a name="discoverobjectactivity-rowset"></a>DISCOVER_OBJECT_ACTIVITY 行集
  提供在启动服务后每个对象的资源使用情况。  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_OBJECT_ACTIVITY`行集包含以下列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`OBJECT_AGGREGATION_HIT`|`DBTYPE_I8`||自服务开始后已命中对象聚合的次数。|  
|`OBJECT_AGGREGATION_MISS`|`DBTYPE_I8`||自服务开始后尚未丢失（即尚未使用）对象现有聚合的次数。|  
|`OBJECT_CPU_TIME_MS`|`DBTYPE_I8`||自服务开始后对象占用的 CPU 时间（毫秒）。|  
|`OBJECT_DATA_VERSION`|`DBTYPE_I4`||对象中数据的沿袭编号；每次处理对象时，此编号随之递增。|  
|`OBJECT_HIT`|`DBTYPE_I8`||自服务开始后缓存中已命中对象的次数。|  
|`OBJECT_ID`|`DBTYPE_WSTR`||创建时定义的对象的 ID|  
|`OBJECT_MISS`|`DBTYPE_I8`||自服务开始后缓存中已丢失对象的次数。|  
|`OBJECT_PARENT_PATH`|`DBTYPE_WSTR`||当前对象的父级的路径。|  
|`OBJECT_READ_KB`|`DBTYPE_I8`||自服务开始后对象读取的数据的累计值 (KB)。|  
|`OBJECT_READS`|`DBTYPE_I8`||自服务开始后对象的累计读取操作数。|  
|`OBJECT_ROWS_RETURNED`|`DBTYPE_I8`||自服务开始后对象返回给调用方的行数。|  
|`OBJECT_ROWS_SCANNED`|`DBTYPE_I8`||自服务开始后对象扫描的行数。|  
|`OBJECT_VERSION`|`DBTYPE_I4`||对象的元数据版本号；每次更改对象时，此编号随之发生变化。|  
|`OBJECT_WRITE_KB`|`DBTYPE_I8`||自服务开始后对象写入的数据的累计值 (KB)。|  
|`OBJECT_WRITES`|`DBTYPE_I8`||自服务开始后对象的累计写入操作数。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 `DISCOVER_OBJECT_ACTIVTY`行集可以限制下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|OBJECT_PARENT_PATH|DBTYPE_WSTR|可选。|  
|OBJECT_ID|DBTYPE_WSTR|可选。|  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis 架构行集](xml-for-analysis-schema-rowsets.md)  
  
  
