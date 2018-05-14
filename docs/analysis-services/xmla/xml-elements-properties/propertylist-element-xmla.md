---
title: PropertyList 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 8d7e92f667ebe37cbdfaf75393bdf2816ef818fd
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="propertylist-element-xmla"></a>PropertyList 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含所使用的 Analysis (XMLA) 属性的集合的 XML[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)和[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Properties>  
   <PropertyList>  
      <!-- Zero or more XMLA properties -->  
   </PropertyList>  
</Properties>  
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
|父元素|[属性](../../../analysis-services/xmla/xml-elements-properties/properties-element-xmla.md)|  
|子元素|XMLA 属性（请参阅“备注”）|  
  
## <a name="remarks"></a>注释  
 **PropertyList** 元素包含一组 XMLA 属性。 利用每个属性，用户可以控制 **Discover** 或 **Execute** 方法的某个方面，如定义连接至数据源所需的信息、指定结果集的返回格式或指定设置数据格式时应使用的区域设置。 **PropertyList** 元素中的每个 XMLA 属性都由单独的 XML 元素定义。 XMLA 属性的值为 XML 元素包含的数据，XMLA 属性的名称与 XML 元素的名称对应。  
  
 结合使用 **Discover** 方法和 DISCOVER_PROPERTIES 请求类型可获取可用属性及其值。 **PropertyList** 元素中列出的属性对顺序没有要求。  
  
 有关支持的 XMLA 属性的详细信息[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]，请参阅[支持 XMLA 属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-supported-xmla-properties.md)。  
  
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
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
