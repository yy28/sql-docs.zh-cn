---
title: "多维数据集元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
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
apiname: Cube Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cube
- urn:schemas-microsoft-com:xml-analysis#Cube
- http://schemas.microsoft.com/analysisservices/2003/engine#Cube
helpviewer_keywords: Cube element
ms.assetid: 2e8662f4-fb2e-43af-b70a-9e0b5872c9b9
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f5099de19e40e38f7e4be4d629aa09fe2cecc671
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="cube-element-xmla"></a>Cube 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]标识包含由父维度的多维数据集[对象](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Object>  
   ...  
   <Cube>...</Cube>  
   ...  
</Object>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[对象](../../../analysis-services/xmla/xml-elements-properties/object-element-dimension-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **多维数据集**元素是包含包含由该维度的多维数据集的名称的对象标识符**对象**元素。  
  
## <a name="see-also"></a>另请参阅  
 [数据库元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/database-element-xmla.md)   
 [维度元素 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/dimension-element-xmla.md)   
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
