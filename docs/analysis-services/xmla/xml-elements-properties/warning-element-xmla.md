---
title: Warning 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bb485e7f8c3df9d1b90ac157940b6c34c0584a5e
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="warning-element-xmla"></a>Warning 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
  包含有关由的实例返回一条警告信息[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Message>  
   <Warning   
      ErrorCode="unsignedint"   
      Severity="string"   
      Description="string"  
      Source="string"  
      HelpFile="string"  
   />  
</Message>  
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
|子元素|无|  
  
## <a name="attributes"></a>属性  
  
|Attribute|说明|  
|---------------|-----------------|  
|ErrorCode|必需的 **UnsignedInt** 属性。 包含警告的数值返回代码。|  
|Severity|可选的 **String** 属性。 包含警告的严重性。|  
|Description|可选的 **String** 属性。 包含警告的说明性文本。|  
|数据源|可选的 **String** 属性。 包含生成警告的组件的名称。|  
|HelpFile|可选的 **String** 属性。 包含到介绍该警告的“帮助”文件或主题的路径或 URL。|  
  
## <a name="remarks"></a>注释  
  
## <a name="see-also"></a>另请参阅  
 [错误元素&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/error-element-xmla.md)   
 [属性 & #40;XMLA & #41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
