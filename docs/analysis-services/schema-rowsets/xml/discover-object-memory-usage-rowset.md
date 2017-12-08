---
title: "DISCOVER_OBJECT_MEMORY_USAGE 行集 |Microsoft 文档"
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
helpviewer_keywords: DISCOVER_OBJECT_MEMORY_USAGE rowset
ms.assetid: 211cfa04-7bd6-43fe-8bd5-bfbff78bdafb
caps.latest.revision: "13"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1a312ed6538be5e639283ade4f77a848ed6e9893
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="discoverobjectmemoryusage-rowset"></a>DISCOVER_OBJECT_MEMORY_USAGE 行集
  提供对象使用的内存资源的相关信息。  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_OBJECT_MEMORY_USAGE**行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**||当前对象的父路径。|  
|**OBJECT_ID**|**DBTYPE_WSTR**||创建时定义的对象的 ID。|  
|**OBJECT_MEMORY_SHRINKABLE**|**是 DBTYPE_I8**||当前对象直接拥有的所有可收缩对象使用的内存总量（字节）。 当前值不包括从归当前对象拥有的命名对象的对象的内存。|  
|**OBJECT_MEMORY_NONSHRINKABLE**|**是 DBTYPE_I8**||当前对象直接拥有的所有不可收缩对象的内存量（字节）。 当前值不包括当前对象拥有的命名对象所拥有的对象的内存。|  
|**OBJECT_VERSION**|**DBTYPE_I4**||对象的元数据版本号。 每次更改对象时，此编号随之发生变化。|  
|**OBJECT_DATA_VERSION**|**DBTYPE_I4**||对象中数据的沿袭编号。 每次处理对象时，此编号随之递增。|  
|**OBJECT_TYPE_ID**|**DBTYPE_I4**||保留以供内部使用。|  
|**OBJECT_TIME_CREATED**|**DBTYPE_DBTIMESTAMP**||创建对象时的 UTC 服务器时间。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 **DISCOVER_OBJECT_MEMORY_USAGE**行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**|可选。|  
|**OBJECT_ID**|**DBTYPE_WSTR**|可选|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
