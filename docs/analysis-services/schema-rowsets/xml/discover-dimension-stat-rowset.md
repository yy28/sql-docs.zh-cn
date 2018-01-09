---
title: "DISCOVER_DIMENSION_STAT 行集 |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
ms.assetid: 639f8cd7-3b43-40d5-8b84-552daf60d484
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 7fb30b200d930a9827aee4b630d80df6e622842e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/08/2018
---
# <a name="discoverdimensionstat-rowset"></a>DISCOVER_DIMENSION_STAT 行集
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]提供有关维度，包括它、 维度名称、 及其属性和每个属性的成员的计数包含的数据库的名称的信息。 在表格模型中，这对应于表中的列和每个列中的值数。  
  
 **适用于：**表格模型、 多维模型  
  
## <a name="rowset-columns"></a>行集列  
 **DISCOVER_DIMENSION_STAT**行集包含以下各列。  
  
|列名|类型指示符|限制|Description|  
|-----------------|--------------------|-----------------|-----------------|  
|**DATABASE_NAME**|**DBTYPE_WSTR**|Required|包含维度的数据库的名称。<br /><br /> 此列在限制列表中是必需的。|  
|**DIMENSION_NAME**|**DBTYPE_WSTR**|Required|维度的名称。<br /><br /> 此列在限制列表中是必需的。|  
|**ATTRIBUTE_NAME**|**DBTYPE_WSTR**||维度中的属性的名称。|  
|**ATTRIBUTE_COUNT**|**是 DBTYPE_I8**||命名属性中的值的计数。 对于表格模型，该值始终等于表中的行数值。|  
  
 未对此架构行集进行排序。  
  
## <a name="using-adomdnet-to-return-the-rowset"></a>使用 ADOMD.NET 返回行集  
 在使用 ADOMD.NET 和架构行集检索元数据时，可以使用 GUID 或字符串在 GetSchemaDataSet 方法中引用架构行集对象。 有关详细信息，请参阅 [Working with Schema Rowsets in ADOMD.NET](../../../analysis-services/multidimensional-models-adomd-net-client/retrieving-metadata-working-with-schema-rowsets.md)。  
  
 下表提供了用于标识此行集的 GUID 和字符串值。  
  
|参数|ReplTest1|  
|--------------|-----------|  
|GUID|a07ccd90-8148-11d0-87bb-00c04fc33942|  
|ADOMDNAME|PartitionDimensionStat|  
  
## <a name="see-also"></a>另请参阅  
 [XML for Analysis 架构行集](../../../analysis-services/schema-rowsets/xml/xml-for-analysis-schema-rowsets.md)  
  
  
