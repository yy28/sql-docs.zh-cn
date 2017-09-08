---
title: "DISCOVER_COMMAND_OBJECTS 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- DISCOVER_COMMAND_OBJECTS rowset
ms.assetid: 325114ee-3a50-4504-9782-dbf7c1a44778
caps.latest.revision: 21
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cae36b0ff5492555137952c2ad9b19f609c53948
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="discovercommandobjects-rowset"></a>DISCOVER_COMMAND_OBJECTS 行集
  提供引用的命令使用的对象的资源使用情况和活动信息。  
  
 **适用于：**表格模型、 多维模型  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_COMMAND_OBJECTS**行集包含以下各列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**SESSION_SPID**|**DBTYPE_I4**|是|会话 ID。|  
|**SESSION_ID**|**DBTYPE_WSTR**|是|会话的唯一标识符，以 GUID 形式表示。|  
|**SESSION_COMMAND_COUNT**|**DBTYPE_I4**||命令的序列号。|  
|**OBJECT_PARENT_PATH**|**DBTYPE_WSTR**|是|当前对象的父路径。|  
|**OBJECT_ID**|**DBTYPE_WSTR**|是|创建时定义的对象 ID。|  
|**OBJECT_VERSION**|**DBTYPE_I4**||对象的元数据版本号；每次更改对象时，此编号随之发生变化。|  
|**OBJECT_DATA_VERSION**|**DBTYPE_I4**||对象中数据的沿袭编号。 每次处理对象时，此编号随之递增。|  
|**OBJECT_CPU_TIME_MS**|**是 DBTYPE_I8**||自命令开始后该对象占用的 CPU 时间（毫秒）。|  
|**OBJECT_READ_KB**|**是 DBTYPE_I8**||自命令开始后对象读取的数据的累计值 (KB)。|  
|**OBJECT_READS**|**是 DBTYPE_I8**||自命令开始后对象的累计读取操作数。|  
|**OBJECT_WRITE_KB**|**是 DBTYPE_I8**||自命令开始后对象写入的数据的累计值 (KB)。|  
|**OBJECT_WRITES**|**是 DBTYPE_I8**||自命令开始后对象的累计写入操作数。|  
|**OBJECT_ROWS_RETURNED**|**是 DBTYPE_I8**||自命令开始后对象返回给调用方的行数。|  
|**OBJECT_ROWS_SCANNED**|**是 DBTYPE_I8**||自命令开始后对象扫描的行数。|  
  
 未对此架构行集进行排序。  
  
> [!IMPORTANT]  
>  DISCOVER_COMMAND_OBJECTS 架构行集不通过 DMV 查询报告活动。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|值|  
|--------------|-----------|  
|GUID|a07ccd35-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|CommandObjects|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
