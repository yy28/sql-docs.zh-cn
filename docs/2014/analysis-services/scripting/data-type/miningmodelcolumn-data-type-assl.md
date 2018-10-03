---
title: MiningModelColumn 数据类型 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MiningModelColumn Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelColumn
helpviewer_keywords:
- MiningModelColumn data type
ms.assetid: de8bf815-43b4-4983-bdb9-b67e8563be0e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b35f260ca14ff416ce5d931457ec741c0736d692
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079457"
---
# <a name="miningmodelcolumn-data-type-assl"></a>MiningModelColumn 数据类型 (ASSL)
  定义一个基元数据类型，表示列中的相关信息[MiningModel](../objects/miningmodel-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModelColumn>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</<Description>  
      <SourceColumnID>...</SourceColumnID>  
            <Usage>...</Usage>  
            <Translations>...</Translations>  
      <Columns>...</Columns>  
      <ModelingFlags>...</ModelingFlags>  
      <Annotations>...</Annotations>  
</MiningModelColumn>  
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
|子元素|[批注](../collections/annotations-element-assl.md)，[列](../collections/columns-element-assl.md)，[说明](../properties/description-element-assl.md)， [ID](../properties/id-element-assl.md)， [ModelingFlags](../collections/modelingflags-element-assl.md)，[名称](../properties/name-element-assl.md)[SourceColumnID](../properties/sourcecolumnid-element-assl.md)，[翻译](../collections/translations-element-assl.md)，[使用情况](../properties/usage-element-dimensionattribute-assl.md)|  
|派生元素|[列](../objects/column-element-assl.md)([列](../collections/columns-element-assl.md)，系列[MiningModel](../objects/miningmodel-element-assl.md))|  
  
## <a name="remarks"></a>备注  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MiningModelColumn>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
