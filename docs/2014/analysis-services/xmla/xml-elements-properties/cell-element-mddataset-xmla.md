---
title: 单元元素 (MDDataSet) (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Cell Element (MDDataSet)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.cell
- http://schemas.microsoft.com/analysisservices/2003/engine#Cell
- urn:schemas-microsoft-com:xml-analysis#Cell
helpviewer_keywords:
- Cell element
ms.assetid: c4ea08a4-f653-4ade-be07-b91eb5b1ef32
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7c422fdd13c03a2ab3c5a9cd58ce4cca1d22c5d6
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091667"
---
# <a name="cell-element-mddataset-xmla"></a>Cell 元素 (MDDataSet) (XMLA)
  包含有关所包含的父级的单个单元格的信息[CellData](celldata-element-xmla.md)元素。  
  
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CellData](celldata-element-xmla.md)|  
|子元素|零个或多个单元属性值或[错误](error-element-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|CellOrdinal|所需`unsignedInt`属性。 多维数据集中单元的序号位置。|  
  
## <a name="remarks"></a>备注  
 在父级 `root` 元素中，`Axes` 元素后跟 `CellData` 元素（包含多维数据集中每个返回单元的属性值的 `Cell` 元素的集合）。 `Cell` 元素包含 `CellOrdinal` 属性（指示该单元在多维数据集中的序号位置，序号从零开始算起）和与该单元关联的每个单元属性值的一个元素。 `Cell` 元素中的每个单元属性值都由单独的 XML 元素定义。 单元属性的值为 XML 元素包含的数据，父级 root 元素的 `CellInfo` 元素中定义的单元属性的名称与 XML 元素的名称对应。  
  
 下列语法对单元属性值进行了说明：  
  
```  
<CellProperty xsi:type="string">value</CellProperty>  
```  
  
 只可为 VALUE 单元属性指定单元属性值的数据类型。 其他单元属性的数据类型由包含在 `CellInfo` 元素中的单元属性定义确定。 如果已为单元属性指定了默认值（方法是将包含在 `Default` 元素中的单元属性定义的 `CellInfo` 元素包括在内），或尚未指定默认值且该单元属性的值为空值，则将不包含单元属性值元素。  
  
## <a name="cell-property-errors"></a>单元属性错误  
 如果由于的实例出现的错误而无法返回单元属性[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，例如阻止向给定单元返回值的计算错误`Error`元素将替换相关单元属性的内容。 下面的 XML 示例介绍了一个单元属性错误：  
  
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
 可以根据 `CellOrdinal` 属性值计算单元的轴引用。 从概念上讲，单元格，像数据集进行编号在数据集中*p*-维数组，其中*p*是轴的数目。 单元按行优先的顺序排列。  
  
 假设某查询请求列中的四个度量值和行中两个州（包含四个地区）的交叉连接。 在下面的数据集结果中，显示为粗体的数据集结果部分的 `CellOrdinal` 属性为 {9, 10, 11, 13, 14, 15, 17, 18, 19}。 结果集之所以为这样，是因为单元是以行优先的顺序编号的，且左上角单元的 `CellOrdinal` 为 0。  
  
|State|季度|Unit sales|Store cost|Store sales|Sales count|  
|-----------|-------------|----------------|----------------|-----------------|-----------------|  
|California|第 1 季度|16890|14431.09|36175.2|5498|  
||第 2 季度|18052|15332.02|38396.75|5915|  
||第 3 季度|18370|**15672.83**|**39394.05**|**6014**|  
||第 4 季度|21436|**18094.5**|**45201.84**|**7015**|  
|Oregon|第 1 季度|19287|**16081.07**|**40170.29**|**6184**|  
||第 2 季度|15079|12678.96|31772.88|4799|  
||第 3 季度|16940|14273.78|35880.46|5432|  
||第 4 季度|16353|13738.68|34453.44|5196|  
|Washington|第 1 季度|30114|25240.08|63282.86|9906|  
||第 2 季度|29479|24953.25|62496.64|9654|  
||第 3 季度|30538|25958.26|64997.38|10007|  
||第 4 季度|34235|29172.72|73016.34|11217|  
  
 应用图中显示的公式，轴 k = 0 具有 Uk = 4 个成员，轴 k = 1 具有 Uk = 8 个元组。 P = 2 是该查询的轴的总数。 将单元 {California, Q3, Store Cost} 视为 S0，初始和为 i = 0 和 1。 对于 i = 0，轴 0 上 {Store Cost} 的元组序号为 1。 对于 i = 1，{CA, Q3} 的元组序号为 2。  
  
 对于我 = 0，Ei = 1，因此，对于我 = 0 总和为 1 * 1 = 1 和我 = 1，总数为 2 （元组序号） 乘以 4 (Ei 的值计算 1 为\*4)，或 8。 最终的总数就为 1 + 8，即 9，这就是该单元的单元序号。  
  
## <a name="example"></a>示例  
 下面的示例演示 `Cell` 元素的结构，其中包括每个单元的 VALUE、FORMATTED_VALUE 和 FORMAT_STRING 单元属性值。  
  
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
  
## <a name="see-also"></a>请参阅  
 [MDDataSet 数据类型&#40;XMLA&#41;](../xml-data-types/mddataset-data-type-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
