---
title: MiningStructure 元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7639078695b80d45f8fc90d6d925ea2335314d15
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="miningstructure-element-assl"></a>MiningStructure 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructures](../../../analysis-services/scripting/collections/miningstructures-element-assl.md)|  
|子元素|[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [CacheMode](../../../analysis-services/scripting/properties/cachemode-element-assl.md)，[排序规则](../../../analysis-services/scripting/properties/collation-element-assl.md)，[列](../../../analysis-services/scripting/collections/columns-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)，[说明](../../../analysis-services/scripting/properties/description-element-assl.md)， [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md)，<br /><br /> [HoldoutActualSize](../../../analysis-services/scripting/properties/holdoutactualsize-element.md)，<br /><br /> [HoldoutMaxCases](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md)，<br /><br /> [HoldoutMaxPercent](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md)，<br /><br /> [HoldoutSeed](../../../analysis-services/scripting/properties/holdoutseed-element.md)，<br /><br /> [ID](../../../analysis-services/scripting/properties/id-element-assl.md)，[语言](../../../analysis-services/scripting/properties/language-element-assl.md)， [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)， [MiningModels](../../../analysis-services/scripting/collections/miningmodels-element-assl.md)， [添加](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)，[源](../../../analysis-services/scripting/properties/source-element-binding-assl.md)，[状态](../../../analysis-services/scripting/properties/state-element-assl.md)，[翻译](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 挖掘结构定义列和绑定。 在定义挖掘结构之后，可以使用该结构来定义多个挖掘模型。 可以对挖掘结构及其所包含的各个挖掘模型进行单独处理。  
  
> [!NOTE]  
>  维持属性中， **HoldoutMaxCases**， **HoldoutMaxPercent**， **HoldoutSeed**，和**HoldoutActualSize**中, 引入了[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. 这些属性使您可以对挖掘结构定义分区，这些分区将用作与该结构关联的所有挖掘模型的测试集。 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 不支持这些属性。 因此，如果您试图对 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 的实例使用这些属性，[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 将返回错误。  
  
## <a name="drillthrough-to-structure-columns"></a>钻取到结构列  
 在[!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]，已将一个新的权限元素添加到[添加元素&#40;ASSL&#41; ](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)集合。 如果你添加**AllowDrillthrough**同时向权限[添加](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)和[MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)集合，从启用钻取功能挖掘模型，以这种方式中的结构，具有的角色的成员**AllowDrillthrough**对模型的权限可以查询数据挖掘模型，并将返回未包含在模型中的结构列。  
  
 因此，为了保护敏感数据或个人信息，你应该构建你的数据源视图来屏蔽敏感信息，并且授予**AllowDrillthrough**仅在必要时的挖掘结构权限。 有关详细信息，请参阅[AllowDrillThrough 元素&#40;ASSL&#41;](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md)。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MiningStructure>。  
  
## <a name="see-also"></a>另请参阅  
 [MiningModel 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)   
 [对象&#40;ASSL&#41;](../../../analysis-services/scripting/objects/objects-assl.md)   
 [选择&AMP;#40;DMX&AMP;#41;](../../../dmx/select-dmx.md)  
  
  
