---
title: "行元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- row Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#row
- microsoft.xml.analysis.row
- http://schemas.microsoft.com/analysisservices/2003/engine#row
helpviewer_keywords:
- row element
ms.assetid: 4d9977a0-c396-44c7-9fd4-97f4c3d643aa
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 52bc6d400340375163fd9ae8b285c071249a88f7
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="row-element-xmla"></a>row 元素 (XMLA)
  包含的数据的单个行[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)包含返回的表格数据元素[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)或[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法调用。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <row>  
      <!-- One or more column elements -->  
   </row>  
</root>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)(使用[行集](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)数据类型)|  
|子元素|一个或多个列元素。|  
  
## <a name="remarks"></a>注释  
 返回每个行**根**包含表格数据元素都有一个相应**行**元素。 每个列中的**根**元素表示由单独的 XML 元素。 为列的值**行**元素是由 XML 元素，包含的数据和列的名称对应于 XML 元素的名称。  
  
 有两种方法可表示行中的列的空值：  
  
-   缺少列元素意味着该列为空。  
  
-   列元素可以使用 `xsi:nil='true'` 属性指示自己具有空值。  
  
 例如，如果某行具有名为 Store_Name 的列，且该列的值为 NULL，则它可以通过以下两种方法之一表示：  
  
```  
<row>  
</row>  
```  
  
 或：  
  
```  
<row>  
   <Store_name xsi:nil='true'/>  
</row>  
```  
  
 如果列元素包含错误，**错误**元素提供有关错误的信息，如下面的示例中所述：  
  
```  
<row>   <Store_name>  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception">  
         <ErrorCode>3238658054</ErrorCode>  
         <Description>The object [X] was not found in the cube when [X] was parsed.</Description>  
      </Error>  
   </Store_name>  
</row>  
```  
  
 有关详细信息列命名和表格数据的架构信息，请参阅[行集数据类型 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md).  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
