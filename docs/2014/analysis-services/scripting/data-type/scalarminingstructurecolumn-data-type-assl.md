---
title: ScalarMiningStructureColumn 数据类型 (ASSL) |Microsoft 文档
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
- ScalarMiningStructureColumn Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ScalarMiningStructureColumn
helpviewer_keywords:
- ScalarMiningStructureColumn data type
ms.assetid: 8f4afc15-601c-4189-bc45-f5a216aed879
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 15e88a5e82dc960e3428587b8d74a046781b90ef
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36126619"
---
# <a name="scalarminingstructurecolumn-data-type-assl"></a>ScalarMiningStructureColumn 数据类型 (ASSL)
  定义一个派生的数据类型，表示[MiningStructureColumn](miningstructurecolumn-data-type-assl.md)包含标量值，而不是与关联的嵌套表的元素[TableMiningStructureColumn](tableminingstructurecolumn-data-type-assl.md)元素包含嵌套的表。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ScalarMiningStructureColumn>  
   <!-- The following elements extend MiningStructureColumn -->  
   <IsKey>...</IsKey>  
   <Source>...</Source>  
   <Distribution>...</Distribution>  
   <ModelingFlags>...</ModelingFlags>  
   <Content>...</Content>  
   <ClassifiedColumnID>...</<ClassifiedColumnI  
   <DiscretizationMethod>...</DiscretizationMethod>  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   <KeyColumns>...</KeyColumns>  
   <NameColumn>...</NameColumn>  
   <Translations>...</Translations>  
</ScalarMiningStructureColumn>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|[MiningStructureColumn](miningstructurecolumn-data-type-assl.md)|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[ClassifiedColumnID](../properties/id-element-assl.md)，[内容](../properties/content-element-assl.md)， [DiscretizationBucketCount](../properties/discretizationbucketcount-element-assl.md)， [DiscretizationMethod](../properties/discretizationmethod-element-assl.md)，[分发](../properties/distribution-element-assl.md)，[IsKey](../properties/iskey-element-assl.md)， [KeyColumns](../collections/columns-element-assl.md)， [ModelingFlags](../collections/modelingflags-element-assl.md)， [NameColumn](../objects/column-element-assl.md)，[源](../properties/source-element-binding-assl.md)， [翻译](../collections/translations-element-assl.md)|  
|派生元素|[列](../objects/column-element-assl.md)([列](../collections/columns-element-assl.md)集合[MiningStructure](../objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  