---
title: DataBlock 数据类型 (ASSL) |Microsoft 文档
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
- DataBlock Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DataBlock
helpviewer_keywords:
- DataBlock data type
ms.assetid: 4192b388-613a-472b-881c-f9c02215aa81
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 12cbd6c1a2723cfc0d9e5b68ff4a484878c82a74
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36026019"
---
# <a name="datablock-data-type-assl"></a>DataBlock 数据类型 (ASSL)
  定义一个基元数据类型，表示用于存储的二进制内容组成的数据块的集合[ClrAssemblyFile](clrassemblyfile-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataBlock>  
   <Blocks>...</Blocks>  
</DataBlock>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|InclusionThresholdSetting|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[块](../collections/blocks-element-assl.md)|  
|派生元素|[数据](../objects/data-element-assl.md)元素[ClrAssemblyFile](clrassemblyfile-data-type-assl.md)类型 ([文件](../collections/files-element-assl.md)集合[ClrAssembly](assembly-data-type-assl.md)类型)|  
  
## <a name="see-also"></a>请参阅  
 [Assembly 元素&#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [文件元素&#40;ASSL&#41;](../objects/file-element-assl.md)   
 [阻止元素&#40;ASSL&#41;](../objects/block-element-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  