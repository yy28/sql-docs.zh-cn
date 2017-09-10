---
title: "单元格元素 (MDDataSet) (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Cell Element (MDDataSet)
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.cell
- http://schemas.microsoft.com/analysisservices/2003/engine#Cell
- urn:schemas-microsoft-com:xml-analysis#Cell
helpviewer_keywords:
- Cell element
ms.assetid: c4ea08a4-f653-4ade-be07-b91eb5b1ef32
caps.latest.revision: 13
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b4d8e85ec05fa6fd8b3c05ee0f27f46b0a28a867
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="cell-element-mddataset-xmla"></a>Cell 元素 (MDDataSet) (XMLA)
  包含有关单个单元格包含父信息[CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CellData>  
   <Cell CellOrdinal="unsignedInt">  
      <!-- Zero or more cell property values -->  
      <!-- or -->  
      <Error>...</Error>  
   </Cell>  
</CellData>  
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
|父元素|[CellData](../../../analysis-services/xmla/xml-elements-properties/celldata-element-xmla.md)|  
|子元素|零个或多个单元格属性值或[错误](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|CellOrdinal|所需**unsignedInt**属性。 多维数据集中单元的序号位置。|  
  
## <a name="remarks"></a>注释  
 在父级中**根**元素，**轴**元素后跟**CellData**元素的一个集合**单元格**包含的元素在多维数据集中返回每个单元格属性值。 **单元格**元素包含**CellOrdinal**属性，它指明的单元格集中的多维数据集，并为每个单元格属性值的一个元素的从零开始的序号位置与单元格关联。 在每个单元格属性值**单元格**由单独的 XML 元素定义元素。 单元格属性的值是 XML 元素和单元格属性的名称包含的数据中定义**CellInfo**父根元素，元素对应于 XML 元素的名称。  
  
 下列语法对单元属性值进行了说明：  
  
```  
<CellProperty xsi:type="string">value</CellProperty>  
```  
  
 只可为 VALUE 单元属性指定单元属性值的数据类型。 其他单元格属性的数据类型由中包含的单元格属性定义**CellInfo**元素。 如果指定默认值，可以排除的单元格属性值元素 (通过包括**默认**单元格属性定义中包含的元素**CellInfo**元素) 的单元格属性，或如果没有默认值已指定并且单元格属性的值为 null。  
  
## <a name="cell-property-errors"></a>单元属性错误  
 如果不能将单元格属性返回因的实例发生的错误而[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，例如防止将值对于给定的单元格，返回的计算错误**错误**元素的问题的单元格属性的内容替换。 下面的 XML 示例介绍了一个单元属性错误：  
  
```  
<Cell CellOrdinal="0">  
   <Value xsi:type="xsd:double">  
      <Error>  
         <ErrorCode>2148497527</ErrorCode>  
         <Description>Unknown error</Description>  
      </Error>  
   </Value>  
</Cell>  
```  
  
## <a name="calculating-cell-ordinal-values"></a>计算单元序号值  
 轴引用单元格，可以计算根据**CellOrdinal**属性值。 从概念上讲，单元格，好像数据集进行编号数据集中*p*-维数组，其中*p*是的轴数。 单元按行优先的顺序排列。  
  
 假设某查询请求列中的四个度量值和行中两个州（包含四个地区）的交叉连接。 以下数据集结果中**CellOrdinal**以粗体显示的数据集结果的一部分的属性是 {9、 10、 11、 13、 14、 15、 17、 18、 19} 组。 这是组，因为单元格按行优先顺序，编号从**CellOrdinal**的左上角单元格的 0。  
  
|State|季度|Unit sales|Store cost|Store sales|Sales count|  
|-----------|-------------|----------------|----------------|-----------------|-----------------|  
|California|Q1|16890|14431.09|36175.2|5498|  
||季 2 季|18052|15332.02|38396.75|5915|  
||第 3 季度|18370|**15672.83**|**39394.05**|**6014**|  
||第 4 季度|21436|**18094.5**|**45201.84**|**7015**|  
|Oregon|Q1|19287|**16081.07**|**40170.29**|**6184**|  
||季 2 季|15079|12678.96|31772.88|4799|  
||第 3 季度|16940|14273.78|35880.46|5432|  
||第 4 季度|16353|13738.68|34453.44|5196|  
|Washington|Q1|30114|25240.08|63282.86|9906|  
||季 2 季|29479|24953.25|62496.64|9654|  
||第 3 季度|30538|25958.26|64997.38|10007|  
||第 4 季度|34235|29172.72|73016.34|11217|  
  
 应用图中显示的公式，轴 k = 0 具有 Uk = 4 个成员，轴 k = 1 具有 Uk = 8 个元组。 P = 2 是该查询的轴的总数。 将单元 {California, Q3, Store Cost} 视为 S0，初始和为 i = 0 和 1。 对于 i = 0，轴 0 上 {Store Cost} 的元组序号为 1。 对于 i = 1，{CA, Q3} 的元组序号为 2。  
  
 为我 = 0，Ei = 1，因此我 = 0 总和是 1 * 1 = 1 和我 = 1，总和是 2 （元组序号） 时间 4 (Ei 的值计算为 1 \* 4)，或 8。 最终的总数就为 1 + 8，即 9，这就是该单元的单元序号。  
  
## <a name="example"></a>示例  
 下面的示例演示了的结构**单元格**元素，包括值、 FORMATTED_VALUE 和 FORMAT_STRING 单元格的每个单元格的属性值。  
  
```  
<CellData>  
   <Cell CellOrdinal="0">  
      <Value xsi:type="xsd:double">16890</Value>  
      <FmtValue>16,890.00</FmtValue>  
      <FormatString>Standard</FormatString>  
   </Cell>  
   <Cell CellOrdinal="1">  
      <Value xsi:type="xsd:int">50</Value>  
      <FmtValue>50</FmtValue>  
      <FormatString>Standard</FormatString>  
   </Cell>  
   <Cell CellOrdinal="2">  
      <Value xsi:type="xsd:double">36175.2</Value>  
      <FmtValue>$36,175.20</FmtValue>  
      <FormatString>Currency</FormatString>  
   </Cell>  
</CellData>  
```  
  
## <a name="see-also"></a>另请参阅  
 [MDDataSet 数据类型 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)   
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
