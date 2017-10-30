---
title: "MdxScript 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MdxScript Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MdxScript
helpviewer_keywords:
- MdxScript element
ms.assetid: 0c59a550-dc95-4d50-948a-bb99348bdd86
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 286b149cf158d08d7da1cc247788ce2591d5099e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="mdxscript-element-assl"></a>MdxScript 元素 (ASSL)
  包含与关联的多维表达式 (MDX) 脚本信息[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MdxScripts>  
   <MdxScript>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</Description>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <Annotations>...</Annotations>  
      <Commands>...</Commands>  
      <DefaultScript>...</DefaultScript>  
      <CalculationProperties>...</CalculationProperties>  
   </MdxScript>  
</MdxScripts>  
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
|父元素|[Mdxscript 被](../../../analysis-services/scripting/collections/mdxscripts-element-assl.md)|  
|子元素|[批注](../../../analysis-services/scripting/collections/annotations-element-assl.md)， [CalculationProperties](../../../analysis-services/scripting/collections/calculationproperties-element-assl.md)，[命令](../../../analysis-services/scripting/collections/commands-element-assl.md)， [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md)， [DefaultScript](../../../analysis-services/scripting/properties/defaultscript-element-assl.md)， [说明](../../../analysis-services/scripting/properties/description-element-assl.md)， [ID](../../../analysis-services/scripting/properties/id-element-assl.md)， [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md)，[名称](../../../analysis-services/scripting/properties/name-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 脚本的**DefaultScript**元素设置为**True**默认情况下。 设置**DefaultScript**到**True**特定的脚本集**DefaultScript**到**False**的所有其他脚本。  
  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MdxScript>。  
  
## <a name="see-also"></a>另请参阅  
 [对象 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

