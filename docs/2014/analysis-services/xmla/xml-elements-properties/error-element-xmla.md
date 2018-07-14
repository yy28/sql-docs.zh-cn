---
title: Error 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Error Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.error
- http://schemas.microsoft.com/analysisservices/2003/engine#Error
- urn:schemas-microsoft-com:xml-analysis#Error
helpviewer_keywords:
- Error element
ms.assetid: add670cb-cab2-42be-91a3-d0c385f29d16
caps.latest.revision: 13
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 55b63c016f9f2c61cc83563e697a49a0c4970cae
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37273733"
---
# <a name="error-element-xmla"></a>Error 元素 (XMLA)
  包含有关错误的实例返回的信息[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
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
|父元素|[Message](message-element-xmla.md)|  
  
## <a name="child-elements"></a>子元素  
  
|Ancestor|子元素|  
|--------------|--------------------|  
|[Message](message-element-xmla.md)|InclusionThresholdSetting|  
|[单元格](cell-element-mddataset-xmla.md)，[行](description-element-xmla.md)， [ErrorCode](errorcode-element-xmla.md)， [HelpFile](file-element-xmla.md)，[源](source-element-error-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|ErrorCode|所需`UnsignedInt`属性 (仅当`Message`是父元素。)包含错误的数值返回代码。|  
|Severity|可选`String`属性 (仅当`Message`是父元素。)包含错误的严重性。|  
|Description|可选`String`属性 (仅当`Message`是父元素。)包含该错误的说明性文本。|  
|数据源|可选`String`属性 (仅当`Message`是父元素。)包含生成该错误的组件的名称。|  
|HelpFile|可选`String`属性 (仅当`Message`是父元素。)包含到介绍该错误的“帮助”文件或主题的路径或 URL。|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>请参阅  
 [Warning 元素&#40;XMLA&#41;](warning-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
