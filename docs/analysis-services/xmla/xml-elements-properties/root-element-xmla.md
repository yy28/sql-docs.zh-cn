---
title: 根元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f4fc4072c7b19cff327463dd8df8af7d136e6c1e
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="root-element-xmla"></a>root 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含返回的结果[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法或的 XML for Analysis (XMLA) 命令执行使用[执行](../../../analysis-services/xmla/xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<return> <!-- or results-->  
   ...  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">...</root> <!-- for Execute method only -->  
   <!-- or -->  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">...</root>  
   <!-- or -->  
   <root xmlns= xmlns="urn:schemas-microsoft-com:xml-analysis:empty">...</root>  
   ...  
</return>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|请参阅下表。|  
|默认值|无|  
|基数|1-n：可多次出现的必需元素。|  
  
|Ancestor|数据类型|  
|--------------|---------------|  
|[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)|[行集](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)， [olapxmla_EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)|  
|[ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)|[MDDataSet](../../../analysis-services/xmla/xml-data-types/mddataset-data-type-xmla.md)，[行集](../../../analysis-services/xmla/xml-data-types/rowset-data-type-xmla.md)， [olapxmla_EmptyResult](../../../analysis-services/xmla/xml-data-types/emptyresult-data-type-xmla.md)|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[结果](../../../analysis-services/xmla/xml-elements-properties/results-element-xmla.md)，[返回](../../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 **根**元素包含在返回的信息[DiscoverResponse](../../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)返回由单个元素**发现**方法调用，或在[ExecuteResponse](../../../analysis-services/xmla/xml-elements-objects-executeresponse.md)返回单个 XMLA 命令执行的单个元素**执行**方法调用。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
