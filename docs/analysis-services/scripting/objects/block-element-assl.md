---
title: 阻止元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9756628a0b766cfa93159daddcdec47ff00f5c66
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="block-element-assl"></a>Block 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含全部或部分二进制内容组成[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Blocks>  
   <Block>...</Block>  
</Blocks>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Base64Binary|  
|默认值|无|  
|基数|1-n：可多次出现的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[块](../../../analysis-services/scripting/collections/blocks-element-assl.md)|  
|子元素|无|  
  
## <a name="see-also"></a>另请参阅  
 [Assembly 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [ClrAssembly 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [文件元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/files-element-assl.md)   
 [文件元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/file-element-assl.md)   
 [ClrAssemblyFile 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)   
 [数据元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/data-element-assl.md)   
 [DataBlock 数据类型 & #40;ASSL & #41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
