---
title: "RestrictionList 元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/04/2017
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
apiname: RestrictionList Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#RestrictionList
- microsoft.xml.analysis.restrictionlist
- http://schemas.microsoft.com/analysisservices/2003/engine#RestrictionList
helpviewer_keywords: RestrictionList element
ms.assetid: 2297c005-381e-49a4-a207-826f7f9ea93a
caps.latest.revision: "11"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 96bbf8798521a6661e630115e5a5669ee24d15df
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="restrictionlist-element-xmla"></a>RestrictionList 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]包含限制列和使用的值的集合[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Restrictions>  
   <RestrictionList>  
      <!-- Zero or more restriction columns and values -->  
   </RestrictionList>  
</Restrictions>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[限制](../../../analysis-services/xmla/xml-elements-properties/restrictions-element-xmla.md)|  
|子元素|限制列和值（请参阅“备注”）。|  
  
## <a name="remarks"></a>注释  
 **RestrictionList** 元素包含限制列的集合，可在这些列上筛选 **Discover** 方法返回的数据。 **RestrictionList** 元素中的每个限制列由一个单独的 XML 元素定义。 限制列的值是 XML 元素中包含的数据，限制列的名称与 XML 元素的名称相对应。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
