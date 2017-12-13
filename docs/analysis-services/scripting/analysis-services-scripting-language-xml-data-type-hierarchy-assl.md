---
title: "Analysis Services 脚本语言 XML 数据类型层次结构 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Analysis Services Scripting Language XML Data Type Hierarchy
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- ASSL, data types
- Analysis Services Scripting Language, data types
- data types [Analysis Services Scripting Language]
- inheritance [Analysis Services Scripting Language]
- hierarchies [Analysis Services Scripting Language]
ms.assetid: f143c9f8-225d-495d-ac8e-ac2d2a7b4c07
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 0ce62ac4aad7532b53c66d34f9d55e2097217fdb
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="analysis-services-scripting-language-xml-data-type-hierarchy-assl"></a>Analysis Services 脚本语言 XML 数据类型层次结构 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]下表显示数据类型的继承层次结构中 Analysis Services 脚本语言 (ASSL)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
Action  
      DrillThroughAction  
      ReportAction  
      StandardAction  
AggregationAttribute  
AggregationDesignAttribute  
AggregationDesignDimension  
AggregationDimension  
Assembly  
      ClrAssembly  
      ComAssembly  
AttributeTranslation  
Binding  
      AttributeBinding  
      ColumnBinding  
      CubeAttributeBinding  
      CubeDimensionBinding  
      DataSourceViewBinding  
      DimensionBinding  
      InheritedBinding  
      MeasureBinding  
      MeasureGroupBinding  
      MeasureGroupDimensionBinding  
      PartitionBinding  
      ProactiveCachingBinding  
            ProactiveCachingIncrementalProcessingBinding  
            ProactiveCachingObjectNotificationBinding  
                  ProactiveCachingInheritedBinding  
                  ProactiveCachingTablesBinding  
            ProactiveCachingQueryBinding  
      RowBinding  
      TabularBinding  
            DSVTableBinding  
            QueryBinding  
            TableBinding  
      TimeAttributeBinding  
      TimeBinding  
      UserDefinedGroupBinding  
ClrAssemblyFile  
CubeAttribute  
CubeBinding (out-of-line)  
CubeDimension  
CubeDimensionPermission  
CubeHierarchy  
DataBlock  
DataItem  
DataMiningMeasureGroupDimension  
DegenerateMeasureGroupDimension  
DimensionAttribute  
EventColumn  
ManyToManyMeasureGroupDimension  
MeasureGroupAttribute  
MeasureGroupBinding (out-of-line)  
MeasureGroupDimension  
MeasureGroupHierarchy  
MiningModelColumn  
MiningModelingFlag  
MiningStructureColumn  
OlapDataSource  
Permission  
PerspectiveAction  
PerspectiveAttribute  
PerspectiveCalculation  
PerspectiveDimension  
PerspectiveHierarchy  
PerspectiveKpi  
PerspectiveMeasure  
PerspectiveMeasureGroup  
PushedDataSource  
ReferenceMeasureGroupDimension  
RegularMeasureGroupDimension  
RelationalDataSource  
ScalarMiningStructureColumn  
TableMiningStructureColumn  
```  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)   
 [Analysis Services 脚本语言 XML 元素层次结构 &#40;ASSL &#41;](../../analysis-services/scripting/analysis-services-scripting-language-xml-element-hierarchy-assl.md)   
 [Analysis Services 脚本语言 &#40;ASSL 为 XMLA &#41;](../../analysis-services/scripting/analysis-services-scripting-language-assl-for-xmla.md)  
  
  
