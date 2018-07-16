---
title: DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS 行集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
ms.assetid: 3e514715-9fe6-4e6a-accb-4149ffd7e0bf
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: ae9955e9f052e4be2317206d5618ccf9294232cb
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37325017"
---
# <a name="discoverstoragetablecolumnsegments-rowset"></a>DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS 行集
  在列级和段级提供有关在表格或 PowerPivot 模式下运行的 Analysis Services 数据库使用的存储表的信息。 此行集主要用于故障排除和分析。  
  
 **适用于：** 表格模型  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS`行集包含以下列。  
  
|**列名**|**类型指示符**|**限制**|**Description**|  
|---------------------|------------------------|---------------------|---------------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|是|指定表格数据库。<br /><br /> `DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS`行集，可通过使用此列进行限制。 如果省略当前数据库使用。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|是|模型的名称。<br /><br /> `DISCOVER_STORAGE_TABLES`行集，可通过使用此列进行限制。|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|是|度量值组的名称。|  
|`PARTITION_NAME`|`DBTYPE_WSTR`|是|分区的名称。|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`||维度的名称。|  
|`TABLE_ID`|`DBTYPE_WSTR`||表段的内部 ID。|  
|`COLUMN_ID`|`DBTYPE_WSTR`||列的内部 ID。|  
|`SEGMENT _NUMBER`|`DBTYPE_I8`||表段的序号。|  
|`TABLE_PARTTION_NUMBER`|`DBTYPE_I8`||分区的序号。|  
|`RECORDS_COUNT`|`DBTYPE_I8`||分区中的记录数。|  
|`ALLOCATED_SIZE`|`DBTYPE_UI8`||分配给列段的大小（字节）。|  
|`USED_SIZE`|`DBTYPE_UI8`||列段使用的大小（字节）。|  
|`COMPRESSION_TYPE`|`DBTYPE_WSTR`||应用于列段的压缩的类型。 该值仅供内部使用及客户支持部门使用。 Microsoft 不发布此列的有效值或说明。|  
|`BITS_COUNT`|`DBTYPE_I8`||位计数。|  
|`BOOKMARK_BITS_COUNT`|`DBTYPE_I8`||书签位计数。|  
|`VERTIPAQ_STATE`|`DBTYPE_WSTR`||此列段的 VertiPaq 压缩状态。 值为以下值之一：<br /><br /> -SKIPPED-已跳过 VertiPaq 压缩。<br />-完成 – VertiPaq 压缩已成功完成。<br />-TIMEBOXED – VertiPaq 压缩已对。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd45-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|StorageSegments|  
  
## <a name="example"></a>示例  
 下面的查询返回与当前数据库中的模型属性 LastName 相关联的存储表段。  
  
```  
SELECT DISTINCT TABLE_ID, COLUMN_ID   
FROM $system.DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS  
WHERE COLUMN_ID = 'LastName'  
ORDER BY TABLE_ID  
  
```  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 架构行集](../analysis-services-schema-rowsets.md)  
  
  
