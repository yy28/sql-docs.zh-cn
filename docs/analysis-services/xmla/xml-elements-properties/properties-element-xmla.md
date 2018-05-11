---
title: Properties 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f185318e3429ccb03b731ff720f0d8f361eac73f
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="properties-element-xmla"></a>properties 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含用于分析 (XMAL) 属性使用的 XML[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)和[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Discover> <!-- or Execute -->  
...  
   <Properties>  
      <PropertyList>...</PropertyList>  
   </Properties>  
...  
</Discover>  
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
|父元素|[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)，[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)|  
|子元素|[PropertyList](../../../analysis-services/xmla/xml-elements-properties/propertylist-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **属性**元素表示用于控制的方面的 XMLA 属性**发现**和**执行**方法，如定义所需的信息连接到数据源，指定该结果集的返回格式或指定应该用于对数据进行格式设置的区域设置。  
  
 结合使用 **Discover** 方法和 DISCOVER_PROPERTIES 请求类型可获取可用属性及其值。  
  
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
  
  
