---
title: 行元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 84cf252303832ed157981103ffaede9718949e16
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34576209"
---
# <a name="row-element-xmla"></a>row 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[根](../../../analysis-services/xmla/xml-elements-properties/root-element-xmla.md)(使用[行集](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)数据类型)|  
|子元素|一个或多个列元素。|  
  
## <a name="remarks"></a>Remarks  
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
  
 有关详细信息列命名和表格数据的架构信息，请参阅[行集数据类型&#40;XMLA&#41;](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)。  
  
## <a name="see-also"></a>另请参阅
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
