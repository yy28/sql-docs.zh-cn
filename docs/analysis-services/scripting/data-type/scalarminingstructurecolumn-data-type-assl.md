---
title: ScalarMiningStructureColumn 数据类型 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9f3544bd99e074c5447d55dd24a42aff69ea3ae1
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="scalarminingstructurecolumn-data-type-assl"></a>ScalarMiningStructureColumn 数据类型 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义一个派生的数据类型，表示[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)包含标量值，而不是与关联的嵌套表的元素[TableMiningStructureColumn](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)包含嵌套的表的元素。  
  
## <a name="syntax"></a>語法  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[ClassifiedColumnID](../../../analysis-services/scripting/properties/classifiedcolumnid-element-assl.md)，[内容](../../../analysis-services/scripting/properties/content-element-assl.md)， [DiscretizationBucketCount](../../../analysis-services/scripting/properties/discretizationbucketcount-element-assl.md)， [DiscretizationMethod](../../../analysis-services/scripting/properties/discretizationmethod-element-assl.md)，[分发](../../../analysis-services/scripting/properties/distribution-element-assl.md)， [IsKey](../../../analysis-services/scripting/properties/iskey-element-assl.md)， [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md)， [ModelingFlags](../../../analysis-services/scripting/collections/modelingflags-element-assl.md)， [NameColumn](../../../analysis-services/scripting/objects/namecolumn-element-assl.md)，[源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)，[翻译](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
|派生元素|[列](../../../analysis-services/scripting/objects/column-element-assl.md)([列](../../../analysis-services/scripting/collections/columns-element-assl.md)集合[MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
