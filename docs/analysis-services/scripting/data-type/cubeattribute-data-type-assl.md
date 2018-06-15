---
title: CubeAttribute 数据类型 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 11a45e49fa902554aaa2b7be1486fb976f03c580
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032138"
---
# <a name="cubeattribute-data-type-assl"></a>CubeAttribute 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义一个基元数据类型，表示与关联的特性[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。  
  
## <a name="syntax"></a>語法  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|无|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[AggregationUsage](../../../analysis-services/scripting/properties/aggregationusage-element-assl.md)，[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [AttributeHierarchyEnabled](../../../analysis-services/scripting/properties/attributehierarchyenabled-element-assl.md)， [AttributeHierarchyOptimizedState](../../../analysis-services/scripting/properties/attributehierarchyoptimizedstate-element-assl.md)， [AttributeHierarchyVisible](../../../analysis-services/scripting/properties/attributehierarchyvisible-element-assl.md)， [AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md)|  
|派生元素|[属性](../../../analysis-services/scripting/objects/attribute-element-assl.md)([属性](../../../analysis-services/scripting/collections/attributes-element-assl.md)集合[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md))|  
  
## <a name="remarks"></a>注释  
 *AttributeHierarchyOptimizedState* deploymentmode 的情况下配置属性值为 1 或 2 中运行服务时，不支持元素 (SharePoint 或表格模式，用于运行[!INCLUDE[ssGemini](../../../includes/ssgemini-md.md)]和表格模型数据库）。  
  
 属性不能添加为层次结构级别时，将该属性*AtttributeHierarchyEnabled*，设置为 FALSE，并且实例在 DeploymentMode 1 或 2 （SharePoint 或表格服务器模式） 下运行。  
  
 中的属性[CubeDimension](../../../analysis-services/scripting/data-type/cubedimension-data-type-assl.md)元素未显式包含在[属性](../../../analysis-services/scripting/collections/attributes-element-assl.md)集合成为属于具有默认值分配给他们的集合。 属性添加到集合之后，可以通过返回的属性[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法。  
  
 [AggregationUsage](../../../analysis-services/scripting/properties/aggregationusage-element-assl.md)元素控件如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]自动设计聚合的属性。 **AggregationUsage**元素不约束任何手动创建的多维数据集的聚合。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.CubeAttribute>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
