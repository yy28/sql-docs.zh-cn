---
title: 文件元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/09/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Files Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Files
helpviewer_keywords:
- Files element
ms.assetid: 8a1327cb-1f60-42a7-b8ef-213d45a63e55
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 5f7556009881e1d4155e47a368bcff4b49aa7988
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36018300"
---
# <a name="files-element-assl"></a>Files 元素 (ASSL)
  包含的集合[文件](../objects/file-element-assl.md)构成元素[ClrAssembly](../data-type/assembly-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Assembly xsi:type="ClrAssembly">  
   ...  
   <Files>  
      <File xsi:type="ClrAssemblyFile">...</File>  
   </Files>  
   ...  
</Assembly>  
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
|父元素|[程序集](../objects/assembly-element-assl.md)类型的[ClrAssembly](../data-type/assembly-data-type-assl.md)|  
|子元素|[文件](../objects/file-element-assl.md)类型的[ClrAssemblyFile](../data-type/clrassemblyfile-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ClrAssemblyFileCollection>。  
  
## <a name="see-also"></a>请参阅  
 [服务器元素&#40;ASSL&#41;](../objects/server-element-assl.md)   
 [数据库元素&#40;ASSL&#41;](../objects/database-element-assl.md)   
 [Assemblies 元素&#40;ASSL&#41;](assemblies-element-assl.md)   
 [数据元素&#40;ASSL&#41;](../objects/data-element-assl.md)   
 [DataBlock 数据类型&#40;ASSL&#41;](../data-type/datablock-data-type-assl.md)   
 [阻止元素&#40;ASSL&#41;](blocks-element-assl.md)   
 [阻止元素&#40;ASSL&#41;](../objects/block-element-assl.md)   
 [ComAssembly 数据类型&#40;ASSL&#41;](../data-type/comassembly-data-type-assl.md)   
 [集合&#40;ASSL&#41;](collections-assl.md)  
  
  