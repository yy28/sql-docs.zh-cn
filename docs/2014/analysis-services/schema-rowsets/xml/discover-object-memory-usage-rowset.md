---
title: DISCOVER_OBJECT_MEMORY_USAGE 行集 |Microsoft 文档
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
- DISCOVER_OBJECT_MEMORY_USAGE rowset
ms.assetid: 211cfa04-7bd6-43fe-8bd5-bfbff78bdafb
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: ae1f26c1bc55c8aa080915a372710e4d59064979
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138948"
---
# <a name="discoverobjectmemoryusage-rowset"></a>DISCOVER_OBJECT_MEMORY_USAGE 行集
  提供对象使用的内存资源的相关信息。  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_OBJECT_MEMORY_USAGE`行集包含以下各列。  
  
|列名|类型指示符|长度|Description|  
|-----------------|--------------------|------------|-----------------|  
|`OBJECT_PARENT_PATH`|`DBTYPE_WSTR`||当前对象的父路径。|  
|`OBJECT_ID`|`DBTYPE_WSTR`||创建时定义的对象的 ID。|  
|`OBJECT_MEMORY_SHRINKABLE`|`DBTYPE_I8`||当前对象直接拥有的所有可收缩对象使用的内存总量（字节）。 当前值不包括从归当前对象拥有的命名对象的对象的内存。|  
|`OBJECT_MEMORY_NONSHRINKABLE`|`DBTYPE_I8`||当前对象直接拥有的所有不可收缩对象的内存量（字节）。 当前值不包括当前对象拥有的命名对象所拥有的对象的内存。|  
|`OBJECT_VERSION`|`DBTYPE_I4`||对象的元数据版本号。 每次更改对象时，此编号随之发生变化。|  
|`OBJECT_DATA_VERSION`|`DBTYPE_I4`||对象中数据的沿袭编号。 每次处理对象时，此编号随之递增。|  
|`OBJECT_TYPE_ID`|`DBTYPE_I4`||保留以供内部使用。|  
|`OBJECT_TIME_CREATED`|`DBTYPE_DBTIMESTAMP`||创建对象时的 UTC 服务器时间。|  
  
 未对此架构行集进行排序。  
  
## <a name="restriction-columns"></a>限制列  
 `DISCOVER_OBJECT_MEMORY_USAGE`行集可限制在下表中列出的列。  
  
|列名|类型指示符|限制状态|  
|-----------------|--------------------|-----------------------|  
|`OBJECT_PARENT_PATH`|`DBTYPE_WSTR`|可选。|  
|`OBJECT_ID`|`DBTYPE_WSTR`|可选|  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis 架构行集](xml-for-analysis-schema-rowsets.md)  
  
  