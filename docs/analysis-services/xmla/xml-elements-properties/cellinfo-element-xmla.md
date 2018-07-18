---
title: CellInfo 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3ada531d33baf7007d08ac8a719fca2bf8f1b2e4
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34574249"
---
# <a name="cellinfo-element-xmla"></a>CellInfo 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  表示单元格元数据包含由容器的父[OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)元素。  
  
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
|父元素|[OlapInfo](../../../analysis-services/xmla/xml-elements-properties/olapinfo-element-xmla.md)|  
|子元素|一个或多个单元属性定义|  
  
## <a name="remarks"></a>Remarks  
 **CellInfo**元素包含单元属性中返回多维数据集包含的单元格的集合**根**元素使用**MDDataSet**数据类型。 每个单元格属性**CellInfo**元素定义由单独的 XML 元素，每个都有**名称**属性和**类型**属性。 **名称**对单元属性的属性对应于的 OLE DB 的 XML 元素中，所表示的 OLAP 单元格属性的名称和**类型**属性表示单元格的 XML 数据类型属性。 XML 元素的名称用于标识的值中包含的单元格的单元格属性**CellData**元素**根**元素。  
  
 下列语法描述了单元属性定义：  
  
```  
<CellPropertyDefinition name="string" type"string" />  
```  
  
 结合使用 **Discover** 方法和 DISCOVER_PROPERTIES 请求类型可获取可用属性及其值。 **PropertyList** 元素中列出的属性对顺序没有要求。  
  
 一个提供程序可以选择指定默认值为中的各个成员或单元格属性**AxisInfo**或**CellInfo**部分。 如果属性总是或几乎总是具有相同的值，则默认值可缩减结果。 若要指示属性的默认值**默认**元素可根据需要指定为一个单元格属性定义元素的子元素。 因此，当结果中缺少某个成员或单元属性时指示声明的默认值是该单元属性的值。  
  
## <a name="example"></a>示例  
 下面的示例演示如何在中表示的值、 FORMATTED_VALUE 和 FORMAT_STRING 单元属性**CellInfo**元素。  
  
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
  
## <a name="see-also"></a>另请参阅
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
