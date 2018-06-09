---
title: 错误元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: f223bff2dced01c2b3f954ca14242b1a35c93813
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/04/2018
ms.locfileid: "34576549"
---
# <a name="error-element-xmla"></a>Error 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含有关错误的 Analysis Services 实例返回的信息。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Message>  
   <Error   
      ErrorCode="unsignedint"   
      Severity="string"   
      Description="string"  
      Source="string"  
      HelpFile="string"  
   />  
</Message>  
<!-- or -->  
<Cell><!-- or row -->  
   <!-- A child element -->  
      <Error xmlns="urn:schemas-microsoft-com:xml-analysis:exception"  
         < ErrorCode>...</ErrorCode>  
         < Description>...</Description>  
         < Source>...</Source>  
         < HelpFile>...</HelpFile>  
      </Error>  
   <!-- /A child element -- >  
</Cell>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Message](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
|子元素|请参阅下表。|  
  
|Ancestor|子元素|  
|--------------|--------------------|  
|[Message](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|InclusionThresholdSetting|  
|[单元格](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md)，[行](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|[说明](../../../analysis-services/xmla/xml-elements-properties/description-element-xmla.md)， [ErrorCode](../../../analysis-services/xmla/xml-elements-properties/errorcode-element-xmla.md)， [HelpFile](../../../analysis-services/xmla/xml-elements-properties/helpfile-element-xmla.md)，[源](../../../analysis-services/xmla/xml-elements-properties/source-element-error-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|ErrorCode|所需**UnsignedInt**属性 (仅当**消息**是父元素。)包含错误的数值返回代码。|  
|Severity|可选**字符串**属性 (仅当**消息**是父元素。)包含错误的严重性。|  
|Description|可选**字符串**属性 (仅当**消息**是父元素。)包含该错误的说明性文本。|  
|数据源|可选**字符串**属性 (仅当**消息**是父元素。)包含生成该错误的组件的名称。|  
|HelpFile|可选**字符串**属性 (仅当**消息**是父元素。)包含到介绍该错误的“帮助”文件或主题的路径或 URL。|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>另请参阅
 [Warning 元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)   
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
