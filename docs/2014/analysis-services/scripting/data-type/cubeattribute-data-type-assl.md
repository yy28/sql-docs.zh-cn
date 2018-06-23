---
title: CubeAttribute 数据类型 (ASSL) |Microsoft 文档
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
api_name:
- CubeAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeAttribute
helpviewer_keywords:
- CubeAttribute data type
ms.assetid: 114ffb44-460b-4971-b31b-dd844e960b81
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: dce594145db99d7edfa991c2e975f62e55d3ef34
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026016"
---
# <a name="cubeattribute-data-type-assl"></a>CubeAttribute 数据类型 (ASSL)
  定义一个基元数据类型，表示与关联的特性[多维数据集](../objects/cube-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CubeAttribute>  
   <AttributeID>...</AttributeID>  
   <AggregationUsage>...</AggregationUsage>  
   <AttributeHierarchyOptimizedState>...</AttributeHierarchyOptimizedState>  
   <AttributeHierarchyEnabled>...</AttributeHierarchyEnabled>  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   <Annotations>...</Annotations>  
</CubeAttribute>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|InclusionThresholdSetting|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[AggregationUsage](../properties/aggregationusage-element-assl.md)，[批注](../collections/annotations-element-assl.md)， [AttributeHierarchyEnabled](../properties/enabled-element-assl.md)， [AttributeHierarchyOptimizedState](../properties/state-element-assl.md)， [AttributeHierarchyVisible](../properties/visible-element-assl.md)， [AttributeID](../properties/id-element-assl.md)|  
|派生元素|[属性](../objects/attribute-element-assl.md)([属性](../collections/attributes-element-assl.md)集合[CubeDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 *AttributeHierarchyOptimizedState*为 1 或 2 (SharePoint 或表格模式，用于运行 PowerPivot 和表格模型数据库） 的属性值在 deploymentmode 的情况下配置中运行服务时，不支持元素。  
  
 属性不能添加为层次结构级别时，将该属性*AtttributeHierarchyEnabled*，设置为 FALSE，并且实例在 DeploymentMode 1 或 2 （SharePoint 或表格服务器模式） 下运行。  
  
 中的属性[CubeDimension](dimension-data-type-assl.md)元素未显式包含在[属性](../collections/attributes-element-assl.md)集合成为属于具有默认值分配给他们的集合。 属性添加到集合之后，可以通过返回的属性[发现](../../xmla/xml-elements-methods-discover.md)方法。  
  
 [AggregationUsage](../properties/aggregationusage-element-assl.md)元素控件如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]自动设计聚合的属性。 `AggregationUsage` 元素不会约束手动为多维数据集创建的任何聚合。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.CubeAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  