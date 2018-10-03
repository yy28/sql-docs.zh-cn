---
title: MiningStructure 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MiningStructure Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningStructure
helpviewer_keywords:
- MiningStructure element
ms.assetid: b943cd92-0ed8-4bd8-8fbc-7dab0534aede
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3d03e52ccb38dc35fada602b6a293d018150efd5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48052087"
---
# <a name="miningstructure-element-assl"></a>MiningStructure 元素 (ASSL)
  定义一组挖掘模型的结构。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructures>  
   <MiningStructure>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</<Description>  
      <Source>...</Source>  
      <CreatedTimestamp>...</<CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastProcessed>...</LastProcessed>  
      <Translations>...</Translations>  
      <Language>...</Language>  
            <Collation>...</Collation>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <CacheMode>...</CacheMode>  
            <Columns>...</Columns>  
      <State>...</State>  
      <HoldoutActualSize>...</HoldoutActualSize>  
      <HoldoutMaxCases>...</HoldoutMaxCases>  
      <HoldoutMaxPercent>...</HoldoutMaxPercent>  
      <HoldoutSeed>...</HoldoutSeed>        
            <MiningStructurePermissions>...</<MiningStructurePermissions>  
            <MiningModels>...</MiningModels>  
            <Annotations>...</Annotations>  
   </MiningStructure>  
</MiningStructures>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructures](../collections/miningstructures-element-assl.md)|  
|子元素|[批注](../collections/annotations-element-assl.md)， [CacheMode](../properties/cachemode-element-assl.md)，[排序规则](../properties/collation-element-assl.md)，[列](../collections/columns-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)，[说明](../properties/description-element-assl.md)， [ErrorConfiguration](errorconfiguration-element-assl.md)，<br /><br /> [HoldoutActualSize](../properties/holdoutactualsize-element.md)，<br /><br /> [HoldoutMaxCases](../properties/holdoutmaxcases-element.md)，<br /><br /> [HoldoutMaxPercent](../properties/holdoutmaxpercent-element.md)，<br /><br /> [HoldoutSeed](../properties/holdoutseed-element.md)，<br /><br /> [ID](../properties/id-element-assl.md)，[语言](../properties/language-element-assl.md)， [LastProcessed](../properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)， [MiningModels](../collections/miningmodels-element-assl.md)， [MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md)，[名称](../properties/name-element-assl.md)，[源](../properties/source-element-binding-assl.md)，[状态](../properties/state-element-assl.md)，[翻译](../collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>备注  
 挖掘结构定义列和绑定。 在定义挖掘结构之后，可以使用该结构来定义多个挖掘模型。 可以对挖掘结构及其所包含的各个挖掘模型进行单独处理。  
  
> [!NOTE]  
>  在 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)] 中引入了以下维持属性：`HoldoutMaxCases`、`HoldoutMaxPercent`、`HoldoutSeed` 和 `HoldoutActualSize`。 这些属性使您可以对挖掘结构定义分区，这些分区将用作与该结构关联的所有挖掘模型的测试集。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 不支持这些属性。 因此，如果您试图对 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的实例使用这些属性，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将返回错误。  
  
## <a name="drillthrough-to-structure-columns"></a>钻取到结构列  
 在中[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]，已添加到新的权限元素[MiningStructurePermissions 元素&#40;ASSL&#41; ](../collections/miningstructurepermissions-element-assl.md)集合。 如果添加`AllowDrillthrough`权同时[MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md)并[MiningModelPermission](miningmodelpermission-element-assl.md)集合，钻取到结构中的方式启用从挖掘模型具有的角色的成员`AllowDrillthrough`对模型的权限可以查询数据挖掘模型，并返回未包含在模型中的结构列。  
  
 因此，若要保护敏感数据或个人信息，应构造数据源视图来屏蔽敏感信息，并且仅在需要时才对挖掘结构授予 `AllowDrillthrough` 权限。 有关详细信息，请参阅[AllowDrillThrough 元素&#40;ASSL&#41;](../properties/allowdrillthrough-element-assl.md)。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MiningStructure>。  
  
## <a name="see-also"></a>请参阅  
 [MiningModel 元素&#40;ASSL&#41;](miningmodel-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)   
 [选择&AMP;#40;DMX&AMP;#41;](/sql/dmx/select-dmx)  
  
  
