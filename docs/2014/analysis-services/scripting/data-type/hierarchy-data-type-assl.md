---
title: 层次结构数据类型 (ASSL) |Microsoft 文档
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
- Hierarchy Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Hierarchy data type
ms.assetid: 2e05917e-7e5d-4dd1-817b-4ff5647747ff
caps.latest.revision: 17
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 14354458e3441c6f8f2691350e9236f2aecb6cdd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138100"
---
# <a name="hierarchy-data-type-assl"></a>Hierarchy 数据类型 (ASSL)
  定义一个表示维度中的层次结构的基元数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Hierarchy>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <DisplayFolder>...</DisplayFolder>  
   <Translations>...</Translations>  
   <AllMemberName>...</AllMemberName>  
   <AllMemberTranslations>...</AllMemberTranslation>  
   <MemberNamesUnique>...</MemberNamesUnique>  
   <AllowDuplicateNames>...</AllowDuplicateNames>  
   <Levels>...</Levels>  
   <Annotations>...</Annotation>  
</Hierarchy>  
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
|子元素|[AllMemberName](../properties/name-element-assl.md)、 [AllMemberTranslations](../collections/translations-element-assl.md)、 [AllowDuplicateNames](../properties/allowduplicatenames-element-assl.md)、 [Annotations](../collections/annotations-element-assl.md)、 [Description](../properties/description-element-assl.md)、 [DisplayFolder](../properties/displayfolder-element-assl.md)、 [ID](../properties/id-element-assl.md)、 [Levels](../collections/levels-element-assl.md)、 [MemberNamesUnique](../properties/membernamesunique-element-assl.md)、 [Name](../properties/name-element-assl.md)、 [Translations](../collections/translations-element-assl.md)|  
|派生元素|[Hierarchy](../objects/hierarchy-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 在 DevelopmentMode 1 或 2 （分别针对 SharePoint 或表格服务器模式）下不支持 *MemberNamesUnique* 元素。  
  
 在 DevelopmentMode 1 或 2 （分别针对 SharePoint 或表格服务器模式）下不支持 *MemberKeysUnique* 元素。  
  
 在 DevelopmentMode 1 或 2 （分别针对 SharePoint 或表格服务器模式）下不支持 *AllowDuplicateNames* 元素。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Hierarchy>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  