---
title: MDDataSet 数据类型 (XMLA) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- MDDataSet Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#MDDataSet
- MDDataSet
- urn:schemas-microsoft-com:xml-analysis#MDDataSet
helpviewer_keywords:
- MDDataSet data type
ms.assetid: 1a7e0092-f9f0-4ae5-ba27-ad1d8ebe8cb9
caps.latest.revision: 27
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 098a123c28e4a449ad6425d1a74ff8355d074e08
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015961"
---
# <a name="mddataset-data-type-xmla"></a>MDDataSet 数据类型 (XMLA)
  定义一个派生的数据类型，表示返回的多维数据[执行](../xml-elements-methods-execute.md)方法。  
  
 **Namespace** urn： 架构-microsoft-com:xml-分析： mddataset  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">  
   <!-- The following elements extend Resultset -->  
   <!-- Optional schema elements -->  
   <OlapInfo>...</OlapInfo>  
   <Axes>...</Axes>  
   <CellData>...</CellData>  
</root>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|[结果集](resultset-data-type-xmla.md)|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[轴](../xml-elements-properties/axes-element-xmla.md)， [CellData](../xml-elements-properties/celldata-element-xmla.md)， [OlapInfo](../xml-elements-properties/olapinfo-element-xmla.md)|  
|派生元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `MDDataSet` 数据类型提供以 XML 表示 OLAP 数据时所需的面向 OLAP 的行集（或数据集）。 值而异的下一个行集合的内容`Content`和`Format`属性中提供[属性](../xml-elements-properties/properties-element-xmla.md)集合`Execute`方法。 有关详细信息`Content`和`Format`属性，请参阅[支持 XMLA 属性&#40;XMLA&#41;](../xml-elements-properties/propertylist-element-supported-xmla-properties.md)。  
  
 有关 OLE DB for OLAP 数据集结构的基本信息，请参考 XML for Analysis 1.1 规范中的“MDDataSet 数据类型到 OLE DB 的映射”。 有关 `MDDataSet` 数据类型的完整 XML 架构定义语言 (XSD) 示例，请参考 XML for Analysis 1.1 规范中的“附录 D：MDDataSet 示例”。  
  
## <a name="see-also"></a>请参阅  
 [XML 数据类型&#40;XMLA&#41;](xml-data-types-xmla.md)  
  
  