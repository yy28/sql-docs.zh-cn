---
title: CellInfo 元素 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CellInfo Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cellinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#CellInfo
- urn:schemas-microsoft-com:xml-analysis#CellInfo
helpviewer_keywords:
- CellInfo element
ms.assetid: 8b6420f1-e9a7-4975-b580-1439fa11f5ca
caps.latest.revision: 13
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 803640fe83ccc3137b4597b8c1b78850abeb55c1
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36029308"
---
# <a name="cellinfo-element-xmla"></a>CellInfo 元素 (XMLA)
  表示单元格元数据包含由容器的父[OlapInfo](olapinfo-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<OlapInfo>  
   ...  
   <CellInfo>  
      <!-- One or more cell property definitions -->  
   </CellInfo>  
   ...  
</OlapInfo>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[OlapInfo](olapinfo-element-xmla.md)|  
|子元素|一个或多个单元属性定义|  
  
## <a name="remarks"></a>Remarks  
 `CellInfo` 元素包含由使用 `root` 数据类型的 `MDDataSet` 元素返回的多维数据集中包含的单元的单元属性集合。 `CellInfo` 元素中的每个单元属性都由单独的 XML 元素定义，每个单元属性都具有 `name` 特性和 `type` 特性。 单元属性的 `name` 特性与 XML 元素表示的 OLE DB for the OLAP 单元属性的名称相对应，而 `type` 特性表示单元属性的 XML 数据类型。 XML 元素的名称用于标识 `CellData` 元素的 `root` 元素中包含的单元的单元属性值。  
  
 下列语法描述了单元属性定义：  
  
```  
<CellPropertyDefinition name="string" type"string" />  
```  
  
 可以通过使用具有的 DISCOVER_PROPERTIES 请求类型获得可用的属性和它们的值`Discover`方法。 `PropertyList` 元素中列出的属性对顺序没有要求。  
  
 访问接口可选择在 `AxisInfo` 部分或 `CellInfo` 部分中指定单个成员或单元属性的默认值。 如果属性总是或几乎总是具有相同的值，则默认值可缩减结果。 若要指示属性的默认值`Default`元素可根据需要指定为一个单元格属性定义元素的子元素。 因此，当结果中缺少某个成员或单元属性时指示声明的默认值是该单元属性的值。  
  
## <a name="example"></a>示例  
 下面的示例演示如何在 `CellInfo` 元素中表示 VALUE、FORMATTED_VALUE 和 FORMAT_STRING 单元属性。  
  
```  
<OlapInfo>  
   ...  
      <CellInfo>  
         <Value name="VALUE"></Value>  
         <FmtValue name="FORMATTED_VALUE"></FmtValue>  
         <FormatString name="FORMAT_STRING"></FormatString>  
      </CellInfo>  
</OlapInfo>  
```  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  