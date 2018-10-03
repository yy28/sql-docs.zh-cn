---
title: row 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- row Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#row
- microsoft.xml.analysis.row
- http://schemas.microsoft.com/analysisservices/2003/engine#row
helpviewer_keywords:
- row element
ms.assetid: 4d9977a0-c396-44c7-9fd4-97f4c3d643aa
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 45bda6938dd98dae305c7143af39fd7d4bfd4142
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48096869"
---
# <a name="row-element-xmla"></a>row 元素 (XMLA)
  包含的数据的单个行[根](root-element-xmla.md)元素，其中包含返回的表格数据[Discover](../xml-elements-methods-discover.md)或[Execute](../xml-elements-methods-execute.md)方法调用。  
  
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
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[根](root-element-xmla.md)(使用[行集](../xml-data-types/rowset-data-type-xmla.md)数据类型)|  
|子元素|一个或多个列元素。|  
  
## <a name="remarks"></a>备注  
 包含表格格式数据的 `root` 元素所返回的每一行都有一个相应的 `row` 元素。 `root` 元素中的每列都由单个 XML 元素表示。 `row` 元素的列值为 XML 元素包含的数据，该列的名称与 XML 元素的名称对应。  
  
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
  
 如果列元素包含错误，则 `Error` 元素可提供有关该错误的信息，如下面的示例所示：  
  
```  
<row>   <Store_name>  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception">  
         <ErrorCode>3238658054</ErrorCode>  
         <Description>The object [X] was not found in the cube when [X] was parsed.</Description>  
      </Error>  
   </Store_name>  
</row>  
```  
  
 有关列命名和表格数据的架构信息，请参阅[行集的数据类型&#40;XMLA&#41;](../xml-data-types/rowset-data-type-xmla.md)。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
