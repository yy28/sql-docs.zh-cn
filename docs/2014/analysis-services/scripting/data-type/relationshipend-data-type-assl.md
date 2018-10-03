---
title: RelationshipEnd 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 3a974dd4-e1d6-45b2-b8c8-1a914bc13a02
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 23d0fce8a0856c178ef6933093400ca67ea4f9d3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48197538"
---
# <a name="relationshipend-data-type-assl"></a>RelationshipEnd 数据类型 (ASSL)
  定义一个基元数据类型，该类型表示关系中的关系方。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<RelationshipEnd>  
   <Role>...</Role>  
   <Multiplicity>...</Multiplicity>  
   <DimensionID>...</DimensionID>  
   <Attributes>...</Attributes>  
   <Translations>...</Translations>  
   <VisualizationProperties>...</VisualizationProperties>  
</Relationship>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|None|  
|派生数据类型|None|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[关系](relationship-data-type-assl.md)|  
|子元素|[角色](../../xmla/xml-elements-properties/role-element-xmla.md)，[多重性](../properties/multiplicity-element-assl.md)， [DimensionID](../properties/id-element-assl.md)，[属性](../collections/attributes-element-assl.md)，[翻译](../collections/translations-element-assl.md)， [VisualizationProperties](relationshipendvisualizationproperties-data-type-assl.md)|  
|派生元素||  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.RelationshipEnd>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
