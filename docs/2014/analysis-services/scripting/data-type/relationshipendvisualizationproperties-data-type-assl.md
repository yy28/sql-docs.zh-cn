---
title: RelationshipEndVisualizationProperties 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 11f9a10f-d36c-4faf-b595-3fe969d1935e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fb59b92c7b0942ce8d8e1c4fd719a8591e6a35cb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48104097"
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
|基本数据类型|None|  
|派生数据类型|None|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[RelationshipEnd](relationshipend-data-type-assl.md)|  
|子元素|[FolderPosition](../../xmla/xml-elements-properties/folderposition-element-xml.md)， [ContextualNameRule](../../xmla/xml-elements-properties/contextualnamerule-element-xml.md)， [DefaultDetailsPosition](../../xmla/xml-elements-properties/defaultdetailsposition-element-xml.md)， [DisplayKeyPosition](../../xmla/xml-elements-properties/displaykeyposition-element-xml.md)， [CommonIdentifierPosition](../../xmla/xml-elements-properties/commonidentifierposition-element-xml.md)， [IsDefaultMeasure](../../xmla/xml-elements-properties/isdefaultmeasure-element-xml.md)， [IsDefaultImage](../../xmla/xml-elements-properties/isdefaultimage-element-xml.md)， [SortPropertiesPosition](../../xmla/xml-elements-properties/sortpropertiesposition-element-xml.md)|  
|派生元素||  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.RelationshipEnd>。  
  
  
