---
title: 类型元素 (ClrAssemblyFile) (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: c41c1661f8a36cb3a76dbcc62e01db9356326cdf
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="type-element-clrassemblyfile-assl"></a>Type 元素 (ClrAssemblyFile) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下列字符串之一：  
  
|“值”|Description|  
|-----------|-----------------|  
|*Main*|指定的文件为程序集中的主文件。|  
|*依赖*|指定的文件为程序集中的依赖文件。|  
|*调试*|指定的文件包含调试信息。|  
  
 对应于的允许值为枚举**类型**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ClrAssemblyFileType>。  
  
 对应于的父元素**类型**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ClrAssemblyFile>。  
  
## <a name="see-also"></a>另请参阅  
 [文件元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/file-element-assl.md)   
 [文件元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/files-element-assl.md)   
 [ClrAssembly 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [Assembly 元素 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
