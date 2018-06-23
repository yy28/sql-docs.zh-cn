---
title: PropertyList 元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- PropertyList Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#PropertyList
- microsoft.xml.analysis.propertylist
- urn:schemas-microsoft-com:xml-analysis#PropertyList
helpviewer_keywords:
- PropertyList element
ms.assetid: 58e63bd9-8aac-438d-adba-1868b4d123f5
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 4b49ad0cf03ce331a00a7eefc9f1302176d89e74
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36014895"
---
# <a name="propertylist-element-xmla"></a>PropertyList 元素 (XMLA)
  包含所使用的 Analysis (XMLA) 属性的集合的 XML[发现](../xml-elements-methods-discover.md)和[执行](../xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Properties>  
   <PropertyList>  
      <!-- Zero or more XMLA properties -->  
   </PropertyList>  
</Properties>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[属性](properties-element-xmla.md)|  
|子元素|XMLA 属性（请参阅“备注”）|  
  
## <a name="remarks"></a>Remarks  
 `PropertyList`元素包含一个 XMLA 属性的集合。 利用每个属性，用户可以控制 `Discover` 或 `Execute` 方法的某个方面，如定义连接至数据源所需的信息、指定结果集的返回格式或指定设置数据格式时应使用的区域设置。 每个 XMLA 属性`PropertyList`由单独的 XML 元素定义元素。 XMLA 属性的值为 XML 元素包含的数据，XMLA 属性的名称与 XML 元素的名称对应。  
  
 可以通过使用具有的 DISCOVER_PROPERTIES 请求类型获得可用的属性和它们的值`Discover`方法。 `PropertyList` 元素中列出的属性对顺序没有要求。  
  
 有关支持的 XMLA 属性的详细信息[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，请参阅[支持 XMLA 属性&#40;XMLA&#41;](propertylist-element-supported-xmla-properties.md)。  
  
## <a name="example"></a>示例  
  
```  
<Properties>  
   <PropertyList>  
      <DataSourceInfo>  
         Provider=MSOLAP;Data Source=local;  
      </DataSourceInfo>  
      <Catalog>  
         Foodmart 2000  
      </Catalog>  
      <Format>  
         Multidimensional  
      </Format>  
   </PropertyList>  
</Properties>  
```  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  