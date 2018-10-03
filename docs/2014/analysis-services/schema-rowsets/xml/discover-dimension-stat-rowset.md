---
title: DISCOVER_DIMENSION_STAT 行集 |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 639f8cd7-3b43-40d5-8b84-552daf60d484
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 39ae0bed8c0e0ff7eb272062b79b870dfb31157e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48094977"
---
# <a name="discoverdimensionstat-rowset"></a>DISCOVER_DIMENSION_STAT 行集
  提供有关维度的信息，包括维度所在的数据库的名称、维度名称、维度的属性以及每个属性的成员计数。 在表格模型中，这对应于表中的列和每个列中的值数。  
  
 **适用于：** 表格模型和多维模型  
  
## <a name="rowset-columns"></a>行集列  
 `DISCOVER_DIMENSION_STAT`行集包含以下列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|`DATABASE_NAME`|`DBTYPE_WSTR`|Required|包含维度的数据库的名称。<br /><br /> 此列在限制列表中是必需的。|  
|`DIMENSION_NAME`|`DBTYPE_WSTR`|Required|维度的名称。<br /><br /> 此列在限制列表中是必需的。|  
|`ATTRIBUTE_NAME`|`DBTYPE_WSTR`||维度中的属性的名称。|  
|`ATTRIBUTE_COUNT`|`DBTYPE_I8`||命名属性中的值的计数。 对于表格模型，该值始终等于表中的行数值。|  
  
 未对此架构行集进行排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../relational-databases/native-client-ole-db-rowsets/rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd90-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>请参阅  
 [XML for Analysis 架构行集](xml-for-analysis-schema-rowsets.md)  
  
  
