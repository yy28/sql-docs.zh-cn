---
title: "DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 3e514715-9fe6-4e6a-accb-4149ffd7e0bf
caps.latest.revision: "15"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 878568721816c90e202727dc3e516370f9c3ee56
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="discoverstoragetablecolumnsegments-rowset"></a>DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]提供在列和段级别表格中运行的 Analysis Services 数据库使用的存储表有关的信息或[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]模式。 此行集主要用于故障排除和分析。  
  
 **适用于：** 表格模型  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS**行集包含以下各列。  
  
|**列名**|**类型指示符**|**限制**|**Description**|  
|---------------------|------------------------|---------------------|---------------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|是|指定表格数据库。<br /><br /> **DISCOVER_STORAGE_TABLE_COLUMN_SEGMENTS**行集可通过使用此列来限制。 如果省略当前数据库使用。|  
|**CUBE_NAME**|**DBTYPE_WSTR**|是|模型的名称。<br /><br /> **DISCOVER_STORAGE_TABLES**行集可通过使用此列来限制。|  
|**MEASURE_GROUP_NAME**|**DBTYPE_WSTR**|是|度量值组的名称。|  
|**PARTITION_NAME**|**DBTYPE_WSTR**|是|分区的名称。|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**||维度的名称。|  
|**针对 TABLE_ID 所**|**DBTYPE_WSTR**||表段的内部 ID。|  
|**COLUMN_ID**|**DBTYPE_WSTR**||列的内部 ID。|  
|**段数目 （_N)**|**是 DBTYPE_I8**||表段的序号。|  
|**TABLE_PARTTION_NUMBER**|**是 DBTYPE_I8**||分区的序号。|  
|**RECORDS_COUNT**|**是 DBTYPE_I8**||分区中的记录数。|  
|**ALLOCATED_SIZE**|**DBTYPE_UI8**||分配给列段的大小（字节）。|  
|**USED_SIZE**|**DBTYPE_UI8**||列段使用的大小（字节）。|  
|**COMPRESSION_TYPE**|**DBTYPE_WSTR**||应用于列段的压缩的类型。 该值仅供内部使用及客户支持部门使用。 Microsoft 不发布此列的有效值或说明。|  
|**BITS_COUNT**|**是 DBTYPE_I8**||位计数。|  
|**BOOKMARK_BITS_COUNT**|**是 DBTYPE_I8**||书签位计数。|  
|**VERTIPAQ_STATE**|**DBTYPE_WSTR**||此列段的 VertiPaq 压缩状态。 值为下列其中一项：<br /><br /> SKIPPED - 已跳过 VertiPaq 压缩。<br /><br /> COMPLETED – VertiPaq 压缩已成功完成。<br /><br /> TIMEBOXED – 已对 VertiPaq 压缩设置时间范围。|  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 架构行集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)  
  
  
