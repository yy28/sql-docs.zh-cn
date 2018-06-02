---
title: Subscribe 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f784cbe3c33eb6b2587b7b535668e793fac3b138
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34574399"
---
# <a name="subscribe-element-xmla"></a>Subscribe 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  订阅跟踪，并返回包含来自 Analysis Services 实例的跟踪事件的行集。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Subscribe>  
      <Object>...</Object>  
   </Subscribe>  
</Command>  
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
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|[对象](../../../analysis-services/xmla/xml-elements-properties/object-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 **订阅**命令订阅和流将从指定的跟踪行集上[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。 如果在 **Object** 元素中指定对象而非跟踪，则会出错。  
  
 如果**对象**元素未指定，则会话跟踪定义，并会在[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。 会话跟踪可从当前会话返回一组固定的跟踪事件。  
  
 客户端应用程序关闭之间的连接将终止此命令返回的行集流[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例，或者，如果在其中的会话**订阅**执行命令会终止。  
  
## <a name="see-also"></a>另请参阅
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
