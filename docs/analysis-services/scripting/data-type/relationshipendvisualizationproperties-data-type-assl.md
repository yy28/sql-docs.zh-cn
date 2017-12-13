---
title: "RelationshipEndVisualizationProperties 数据类型 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
applies_to: SQL Server 2016 Preview
ms.assetid: 11f9a10f-d36c-4faf-b595-3fe969d1935e
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2a7f01678ae4dbac56e6a7e09a2818d6c4dac49e
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="relationshipendvisualizationproperties-data-type-assl"></a>RelationshipEndVisualizationProperties 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]定义表示关系中的关系端的基元数据类型。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|无|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[RelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md)|  
|子元素|[FolderPosition](../../../analysis-services/xmla/xml-elements-properties/folderposition-element-xml.md)， [ContextualNameRule](../../../analysis-services/xmla/xml-elements-properties/contextualnamerule-element-xml.md)， [DefaultDetailsPosition](../../../analysis-services/xmla/xml-elements-properties/defaultdetailsposition-element-xml.md)， [DisplayKeyPosition](../../../analysis-services/xmla/xml-elements-properties/displaykeyposition-element-xml.md)， [CommonIdentifierPosition](../../../analysis-services/xmla/xml-elements-properties/commonidentifierposition-element-xml.md)， [IsDefaultMeasure](../../../analysis-services/xmla/xml-elements-properties/isdefaultmeasure-element-xml.md)， [IsDefaultImage](../../../analysis-services/xmla/xml-elements-properties/isdefaultimage-element-xml.md)， [SortPropertiesPosition](../../../analysis-services/xmla/xml-elements-properties/sortpropertiesposition-element-xml.md)|  
|派生元素||  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.RelationshipEnd>。  
  
  
