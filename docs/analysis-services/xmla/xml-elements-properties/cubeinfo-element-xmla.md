---
title: "CubeInfo 元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services, azure-analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: CubeInfo Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#CubeInfo
- microsoft.xml.analysis.cubeinfo
- urn:schemas-microsoft-com:xml-analysis#CubeInfo
helpviewer_keywords: CubeInfo element
ms.assetid: a504bac5-4bf2-4f78-a288-e74a34eaa97e
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: b6d12adc4fb3f9ac59d2af3855cfbb0417ce9a14
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="cubeinfo-element-xmla"></a>CubeInfo 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]包含多维数据集的元数据包含由容器的父[OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<OlapInfo>  
   ...  
   <CubeInfo>  
      <Cube>...</Cube>  
   </CubeInfo>  
   ...  
</OlapInfo>  
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
|父元素|[OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|子元素|[Cube](../../../analysis-services/xmla/xml-elements-properties/cube-element-olapinfo-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **CubeInfo**元素包含一个**多维数据集**为在多维数据集中引用的每个多维数据集的元素。  
  
> [!NOTE]  
>  [!INCLUDE[msCoName](../../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]返回只有一个**多维数据集**此集合中的元素因为[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]不支持语句引用的多维表达式 （的 FROM 子句中的多个多维数据集MDX) 语言。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
