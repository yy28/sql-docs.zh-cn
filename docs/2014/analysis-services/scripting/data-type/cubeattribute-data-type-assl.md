---
title: CubeAttribute 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d64224c1b7489895ff0d9dca00a3841be0ed0bbc
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48203297"
---
# <a name="cubeattribute-data-type-assl"></a>CubeAttribute 数据类型 (ASSL)
  定义一个基元数据类型，表示与关联的属性[多维数据集](../objects/cube-element-assl.md)元素。  
  
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
|基本数据类型|None|  
|派生数据类型|None|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[AggregationUsage](../properties/aggregationusage-element-assl.md)，[批注](../collections/annotations-element-assl.md)， [AttributeHierarchyEnabled](../properties/enabled-element-assl.md)， [AttributeHierarchyOptimizedState](../properties/state-element-assl.md)， [AttributeHierarchyVisible](../properties/visible-element-assl.md)， [AttributeID](../properties/id-element-assl.md)|  
|派生元素|[特性](../objects/attribute-element-assl.md)([特性](../collections/attributes-element-assl.md)的集合[CubeDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>备注  
 *AttributeHierarchyOptimizedState*在 DeploymentMode 配置属性值为 1 或 2 （SharePoint 或表格模式，用于运行 PowerPivot 和表格模型数据库） 运行服务时，不支持元素。  
  
 属性不能作为层次结构级别添加时属性， *AtttributeHierarchyEnabled*，设置为 FALSE 并且该实例正在 DeploymentMode 1 或 2 （SharePoint 或表格服务器模式） 下操作。  
  
 中的属性[CubeDimension](dimension-data-type-assl.md)未显式包含在元素[属性](../collections/attributes-element-assl.md)集合变得具有分配给它们的默认值的集合的一部分。 属性添加到集合后，可以通过返回属性[发现](../../xmla/xml-elements-methods-discover.md)方法。  
  
 [AggregationUsage](../properties/aggregationusage-element-assl.md)元素控制如何[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]自动设计属性的聚合。 `AggregationUsage` 元素不会约束手动为多维数据集创建的任何聚合。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.CubeAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
