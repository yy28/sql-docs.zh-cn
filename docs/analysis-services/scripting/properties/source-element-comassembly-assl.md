---
title: "源元素 (ComAssembly) (ASSL) |Microsoft 文档"
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
apiname: Source Element (ComAssembly)
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Source
helpviewer_keywords: Source element
ms.assetid: 5c9209e8-ace6-4688-a64d-4987a7648ab9
caps.latest.revision: "38"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f9982e379b56374da92a5b672da24e591603a0a9
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="source-element-comassembly-assl"></a>Source 元素 (ComAssembly) (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]包含的文件名称或组件对象模型 (COM) 组件的编程标识符 (ProgID)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ComAssembly>  
   ...  
   <Source>...</Source>  
   ...  
</ComAssembly>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ComAssembly](../../../analysis-services/scripting/data-type/comassembly-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**源**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ComAssembly>。  
  
## <a name="see-also"></a>另请参阅  
 [Assembly 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/assembly-element-assl.md)   
 [ClrAssembly 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/clrassembly-data-type-assl.md)   
 [Assemblies 元素 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/assemblies-element-assl.md)   
 [数据库元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/database-element-assl.md)   
 [服务器元素 &#40;ASSL &#41;](../../../analysis-services/scripting/objects/server-element-assl.md)   
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
