---
title: "文件元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Files Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Files
helpviewer_keywords: Files element
ms.assetid: 8a1327cb-1f60-42a7-b8ef-213d45a63e55
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 2b66a33f8586eb035f38387d111803f0d32a85d3
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="files-element-assl"></a>Files 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含的集合[文件](../../../analysis-services/scripting/objects/file-element-assl.md)构成元素[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)元素。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[程序集](../../../analysis-services/scripting/objects/assembly-element-assl.md)类型的[ClrAssembly](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)|  
|子元素|[文件](../../../analysis-services/scripting/objects/file-element-assl.md)类型的[ClrAssemblyFile](../../../analysis-services/scripting/data-type/clrassemblyfile-data-type-assl.md)|  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.ClrAssemblyFileCollection>。  
  
## <a name="see-also"></a>另请参阅  
 [服务器元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [数据库元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [Assemblies 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [数据元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/data-element-assl.md)   
 [DataBlock 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/datablock-data-type-assl.md)   
 [块元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/blocks-element-assl.md)   
 [块元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/block-element-assl.md)   
 [ComAssembly 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)   
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
