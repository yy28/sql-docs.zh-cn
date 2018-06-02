---
title: 语句元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 49238b50457a586bbf23cc75ee454003c57ac04e
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34575019"
---
# <a name="statement-element-xmla"></a>Statement 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含查询或语句发送使用**执行**到的 Analysis Services 实例的方法。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Command>  
   <Statement>...</Statement>  
</Command>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Command](../../../analysis-services/xmla/xml-elements-properties/command-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **语句**命令上执行查询或语句[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例。 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 支持以下语言：  
  
-   多维表达式 (MDX)  
  
-   数据挖掘扩展插件 (MDX)  
  
-   结构化查询语言 (SQL) 的子集  
  
## <a name="see-also"></a>另请参阅
 [命令&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-commands/xml-elements-commands.md)  
  
  
