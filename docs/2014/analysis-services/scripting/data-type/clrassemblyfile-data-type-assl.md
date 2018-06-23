---
title: ClrAssemblyFile 数据类型 (ASSL) |Microsoft 文档
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
- ClrAssemblyFile Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ClrAssemblyFile
helpviewer_keywords:
- ClrAssemblyFile data type
ms.assetid: 91074677-c149-483b-a56d-0e35d959d9eb
caps.latest.revision: 41
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b542c4193d80fa80cc9aed6663f41e102266000b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017205"
---
# <a name="clrassemblyfile-data-type-assl"></a>ClrAssemblyFile 数据类型 (ASSL)
  定义一个基元数据类型，表示组成的文件之一[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] `Assembly` ([ClrAssembly](assembly-data-type-assl.md)元素)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ClrAssemblyFile>  
   <Name>...</Name>  
      <Type>...</Type>  
      <Data>...</Data>  
</ClrAssemblyFile>  
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
|子元素|[数据](../objects/data-element-assl.md)，[名称](../properties/name-element-assl.md)，[类型](../properties/type-element-clrassemblyfile-assl.md)|  
|派生元素|[文件](../objects/file-element-assl.md)([文件](../collections/files-element-assl.md)集合[ClrAssembly](assembly-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ClrAssemblyFile>。  
  
## <a name="see-also"></a>请参阅  
 [服务器元素&#40;ASSL&#41;](../objects/server-element-assl.md)   
 [数据库元素&#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [Assembly 元素&#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [DataBlock 数据类型&#40;ASSL&#41;](datablock-data-type-assl.md)   
 [阻止元素&#40;ASSL&#41;](../collections/blocks-element-assl.md)   
 [阻止元素&#40;ASSL&#41;](../objects/block-element-assl.md)   
 [ComAssembly 数据类型&#40;ASSL&#41;](comassembly-data-type-assl.md)   
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  