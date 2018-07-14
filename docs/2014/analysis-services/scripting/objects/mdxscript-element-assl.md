---
title: MdxScript 元素 (ASSL) |Microsoft Docs
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
- MdxScript Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MdxScript
helpviewer_keywords:
- MdxScript element
ms.assetid: 0c59a550-dc95-4d50-948a-bb99348bdd86
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3aa8d72073f5459a7e260a81ca4bf5c67ad3209b
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37169468"
---
# <a name="mdxscript-element-assl"></a>MdxScript 元素 (ASSL)
  包含有关与相关联的多维表达式 (MDX) 脚本的信息[多维数据集](cube-element-assl.md)元素。  
  
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MdxScripts](../collections/mdxscripts-element-assl.md)|  
|子元素|[批注](../collections/annotations-element-assl.md)， [CalculationProperties](../collections/calculationproperties-element-assl.md)，[命令](../collections/commands-element-assl.md)， [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)， [DefaultScript](../properties/defaultscript-element-assl.md)， [说明](../properties/description-element-assl.md)， [ID](../properties/id-element-assl.md)， [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)，[名称](../properties/name-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 默认情况下，脚本的 `DefaultScript` 元素设置为 `True`。 将特定脚本的 `DefaultScript` 设置为 `True` 将使所有其他脚本的 `DefaultScript` 设置为 `False`。  
  
 在 Analysis Management Objects (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.MdxScript>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
