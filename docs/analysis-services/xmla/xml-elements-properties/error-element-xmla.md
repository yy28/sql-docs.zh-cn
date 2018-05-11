---
title: 错误元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: a9903e86d5931d92222aec00f3896a2db78732f5
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="error-element-xmla"></a>Error 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含有关 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]实例返回的错误的信息。  
  
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
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[消息](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|  
|子元素|请参阅下表。|  
  
|Ancestor|子元素|  
|--------------|--------------------|  
|[消息](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|无|  
|[Cell](../../../analysis-services/xmla/xml-elements-properties/cell-element-mddataset-xmla.md)、 [row](../../../analysis-services/xmla/xml-elements-properties/message-element-xmla.md)|[Description](../../../analysis-services/xmla/xml-elements-properties/description-element-xmla.md)、 [ErrorCode](../../../analysis-services/xmla/xml-elements-properties/errorcode-element-xmla.md)、 [HelpFile](../../../analysis-services/xmla/xml-elements-properties/helpfile-element-xmla.md)、 [Source](../../../analysis-services/xmla/xml-elements-properties/source-element-error-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|说明|  
|---------------|-----------------|  
|ErrorCode|所需**UnsignedInt**属性 (仅当**消息**是父元素。)包含错误的数值返回代码。|  
|Severity|可选**字符串**属性 (仅当**消息**是父元素。)包含错误的严重性。|  
|Description|可选**字符串**属性 (仅当**消息**是父元素。)包含该错误的说明性文本。|  
|数据源|可选**字符串**属性 (仅当**消息**是父元素。)包含生成该错误的组件的名称。|  
|HelpFile|可选**字符串**属性 (仅当**消息**是父元素。)包含到介绍该错误的“帮助”文件或主题的路径或 URL。|  
  
## <a name="remarks"></a>備註  
  
## <a name="see-also"></a>另请参阅  
 [Warning 元素 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/warning-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
