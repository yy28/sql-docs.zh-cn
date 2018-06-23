---
title: DISCOVER_PARTITION_STAT 行集 |Microsoft 文档
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
ms.assetid: 20d339e2-f47f-437f-94d5-5b00b400356a
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 98db8d43f86cc9acaf612da8180498d22e01d037
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36137625"
---
# <a name="discoverpartitionstat-rowset"></a>DISCOVER_PARTITION_STAT 行集
  返回特定分区中的聚合的统计信息。  
  
 **适用于：** 表格模型、 多维模型  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_PARTITION_STAT`行集包含以下各列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|Required|包含维度的数据库的名称。<br /><br /> 此列在限制列表中是必需的。|  
|`CUBE_NAME`|`DBTYPE_WSTR`|Required|包含分区的多维数据集或表格模型的名称。<br /><br /> 此列在限制列表中是必需的。|  
|`MEASURE_GROUP_NAME`|`DBTYPE_WSTR`|Required|维度中的度量值组的名称。<br /><br /> 此列在限制列表中是必需的。|  
|`PARTITION_NAME`|`DBTYPE_WSTR`|Required|分区的名称。<br /><br /> 此列在限制列表中是必需的。|  
|`AGGREGATION_NAME`|`DBTYPE_WSTR`||聚合的名称。|  
|`AGGREGATION_SIZE`|`DBTYPE_I8`||聚合的大小。|  
  
 未对此架构行集进行排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd8f-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionStat|  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis 架构行集](xml-for-analysis-schema-rowsets.md)  
  
  