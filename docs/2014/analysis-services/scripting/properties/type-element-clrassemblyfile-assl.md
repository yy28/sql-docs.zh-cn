---
title: Type 元素 (ClrAssemblyFile) (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7f5f52857fd9e87541e07ee03ffd36a7b24a4e96
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48140377"
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
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 此元素的值限定为下列字符串之一：  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|*Main*|指定的文件为程序集中的主文件。|  
|*依赖*|指定的文件为程序集中的依赖文件。|  
|*调试*|指定的文件包含调试信息。|  
  
 与允许的值相对应的枚举`Type`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ClrAssemblyFileType>。  
  
 父级对应的元素`Type`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.ClrAssemblyFile>。  
  
## <a name="see-also"></a>请参阅  
 [文件元素&#40;ASSL&#41;](../objects/file-element-assl.md)   
 [文件元素&#40;ASSL&#41;](../collections/files-element-assl.md)   
 [ClrAssembly 数据类型&#40;ASSL&#41;](../data-type/assembly-data-type-assl.md)   
 [Assembly 元素&#40;ASSL&#41;](../objects/assembly-element-assl.md)   
 [程序集元素&#40;ASSL&#41;](../collections/assemblies-element-assl.md)   
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
