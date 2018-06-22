---
title: 类型元素 (ClrAssemblyFile) (ASSL) |Microsoft 文档
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
- Type Element (ClrAssemblyFile)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: ab9e1e2c-ab06-4cd1-b007-16d738dc5604
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: c253b2975c5e4f4cbf27c5b2d655a09617d644de
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014390"
---
# <a name="type-element-clrassemblyfile-assl"></a>Type 元素 (ClrAssemblyFile) (ASSL)
  指定一个属于文件的文件类型[!INCLUDE[msCoName](../../../includes/msconame-md.md)].NET Framework 程序集。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ClrAssemblyFile>  
      ...  
      <Type>...</Type>  
   ...  
</ClrAssemblyFile>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 此元素的值限定为下列字符串之一：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*Main*|指定的文件为程序集中的主文件。|  
|*依赖*|指定的文件为程序集中的依赖文件。|  
|*调试*|指定的文件包含调试信息。|  
  
 对应于的允许值为枚举`Type`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ClrAssemblyFileType>。  
  
 对应于的父元素`Type`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ClrAssemblyFile>。  
  
## <a name="see-also"></a>请参阅  
 [文件元素&#40;ASSL&#41;](../objects/file-element-assl.md)   
 [文件元素&#40;ASSL&#41;](../collections/files-element-assl.md)   
 [ClrAssembly 数据类型&#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [Assembly 元素&#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  