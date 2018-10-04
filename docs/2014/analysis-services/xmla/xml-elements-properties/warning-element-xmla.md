---
title: Warning 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Warning Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Warning
- microsoft.xml.analysis.warning
- http://schemas.microsoft.com/analysisservices/2003/engine#Warning
helpviewer_keywords:
- Warning element
ms.assetid: a34a6caa-4b68-486b-8f50-cdc124c65888
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9f0dfa8e3cc45291a32885674fe5f77145aca2f0
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079887"
---
# <a name="warning-element-xmla"></a>Warning 元素 (XMLA)
  包含有关的实例返回一条警告信息[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。  
  
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Message](message-element-xmla.md)|  
|子元素|None|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|ErrorCode|所需`UnsignedInt`属性。 包含警告的数值返回代码。|  
|Severity|可选`String`属性。 包含警告的严重性。|  
|Description|可选`String`属性。 包含警告的说明性文本。|  
|数据源|可选`String`属性。 包含生成警告的组件的名称。|  
|HelpFile|可选`String`属性。 包含到介绍该警告的“帮助”文件或主题的路径或 URL。|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [错误元素&#40;XMLA&#41;](error-element-xmla.md)   
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
