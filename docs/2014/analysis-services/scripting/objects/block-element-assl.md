---
title: Block 元素 (ASSL) |Microsoft Docs
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
- Block Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Block
helpviewer_keywords:
- Block element
ms.assetid: f45c32ae-e4e0-465a-9564-9ccfb10a858f
caps.latest.revision: 36
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 44022a2e0bd538b7f4b33b0d1f1fb7b462e676e6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37279433"
---
# <a name="block-element-assl"></a>Block 元素 (ASSL)
  包含全部或部分二进制内容组成[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Blocks>  
   <Block>...</Block>  
</Blocks>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Base64Binary|  
|默认值|InclusionThresholdSetting|  
|基数|1-n：可多次出现的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[块](../collections/blocks-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="see-also"></a>请参阅  
 [Assembly 元素&#40;ASSL&#41;](assembly-element-assl.md)   
 [ClrAssembly 数据类型&#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [文件元素&#40;ASSL&#41;](../collections/files-element-assl.md)   
 [文件元素&#40;ASSL&#41;](file-element-assl.md)   
 [ClrAssemblyFile 数据类型&#40;ASSL&#41;](../data-type/clrassemblyfile-data-type-assl.md)   
 [数据元素&#40;ASSL&#41;](data-element-assl.md)   
 [DataBlock 数据类型&#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
