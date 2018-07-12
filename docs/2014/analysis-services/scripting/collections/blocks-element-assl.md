---
title: 阻止元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Blocks Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Blocks
helpviewer_keywords:
- Blocks element
ms.assetid: d6fd4e6b-b5bd-43cd-9c28-48af57cf977c
caps.latest.revision: 32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: c2776ea261c26bd8c53d3f78ba29231823bb659d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37161318"
---
# <a name="blocks-element-assl"></a>Blocks 元素 (ASSL)
  包含表示的二进制内容的二进制数据块的集合[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Data xsi:type="DataBlock">  
   ...  
   <Blocks>  
      <Block>...</Block>  
   </Blocks>  
   ...  
</File>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[数据](../objects/data-element-assl.md)类型的[DataBlock](../data-type/datablock-data-type-assl.md)|  
|子元素|[块](../objects/block-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 父级对应的元素`Blocks`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ClrAssemblyFile>。  
  
## <a name="see-also"></a>请参阅  
 [Assembly 元素&#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [ClrAssembly 数据类型&#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [文件元素&#40;ASSL&#41;](files-element-assl.md)   
 [文件元素&#40;ASSL&#41;](../objects/file-element-assl.md)   
 [ClrAssemblyFile 数据类型&#40;ASSL&#41;](../data-type/clrassemblyfile-data-type-assl.md)   
 [数据元素&#40;ASSL&#41;](../objects/data-element-assl.md)   
 [DataBlock 数据类型&#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [Blocks 元素](blocks-element-assl.md)   
 [Block 元素&#40;ASSL&#41;](../objects/block-element-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  
