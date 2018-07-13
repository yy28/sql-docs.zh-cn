---
title: RelationshipEndVisualizationProperties 数据类型 (ASSL) |Microsoft Docs
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
ms.assetid: 11f9a10f-d36c-4faf-b595-3fe969d1935e
caps.latest.revision: 5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 58348251e9ea00c4f6eebc5fcec067683e49a3a2
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161268"
---
# <a name="relationshipendvisualizationproperties-data-type-assl"></a>RelationshipEndVisualizationProperties 数据类型 (ASSL)
  定义一个基元数据类型，该类型表示关系中的关系方。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<RelationshipEnd>  
   <FolderPosition>...</FolderPosition>  
   <ContextualNameRule>...</ContextualNameRule>  
   <DefaultDetailsPosition>...</DefaultDetailsPosition>  
   <DisplayKeyPosition>...</DisplayKeyPosition>  
   <CommonIdentifierPosition>...</CommonIdentifierPosition>  
   <IsDefaultMeasure>...</IsDefaultMeasure>  
   <IsDefaultImage>...</IsDefaultImage>  
   <SortPropertiesPosition>...</SortPropertiesPosition>  
</RelationshipEnd>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|InclusionThresholdSetting|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[RelationshipEnd](relationshipend-data-type-assl.md)|  
|子元素|[FolderPosition](../../xmla/xml-elements-properties/folderposition-element-xml.md)， [ContextualNameRule](../../xmla/xml-elements-properties/contextualnamerule-element-xml.md)， [DefaultDetailsPosition](../../xmla/xml-elements-properties/defaultdetailsposition-element-xml.md)， [DisplayKeyPosition](../../xmla/xml-elements-properties/displaykeyposition-element-xml.md)， [CommonIdentifierPosition](../../xmla/xml-elements-properties/commonidentifierposition-element-xml.md)， [IsDefaultMeasure](../../xmla/xml-elements-properties/isdefaultmeasure-element-xml.md)， [IsDefaultImage](../../xmla/xml-elements-properties/isdefaultimage-element-xml.md)， [SortPropertiesPosition](../../xmla/xml-elements-properties/sortpropertiesposition-element-xml.md)|  
|派生元素||  
  
## <a name="remarks"></a>Remarks  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.RelationshipEnd>。  
  
  
