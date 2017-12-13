---
title: "其中元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
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
apiname: Where Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Where
- microsoft.xml.analysis.where
- http://schemas.microsoft.com/analysisservices/2003/engine#Where
helpviewer_keywords: Where element
ms.assetid: 81fb4190-3379-4ddf-8795-a0772f3b92bb
caps.latest.revision: "12"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 50050fc4845161f18568aeb92e8bc4bb1ab49026
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/08/2017
---
# <a name="where-element-xmla"></a>Where 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]定义由容器的父使用的筛选条件[删除](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)或[更新](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)命令。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Drop> <!-- or Update -->  
   ...  
   <Where>  
      <Attributes>...</Attributes>  
   </Where>  
   ...  
</Insert>  
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
|父元素|[Drop](../../../analysis-services/xmla/xml-elements-commands/drop-element-xmla.md)、 [Update](../../../analysis-services/xmla/xml-elements-commands/update-element-xmla.md)|  
|子元素|[属性](../../../analysis-services/xmla/xml-elements-properties/attributes-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 对于 **Drop** 命令， **Where** 元素与 [DeleteWithDescendants](../../../analysis-services/xmla/xml-elements-properties/deletewithdescendants-element-xmla.md) 元素结合使用，可标识要删除的属性成员的范围。  
  
 对于 **Update** 命令， **Where** 元素标识要更新的属性成员的范围。 结合使用父 **Attributes** 命令的 **Update** 集合和 **Attributes** 元素的 **Where** 集合中的属性可更新多个属性成员。  
  
 有关删除和更新属性成员的详细信息，请参阅[插入、更新和删除成员 (XMLA)](../../../analysis-services/multidimensional-models-scripting-language-assl-xmla/inserting-updating-and-dropping-members-xmla.md)。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
