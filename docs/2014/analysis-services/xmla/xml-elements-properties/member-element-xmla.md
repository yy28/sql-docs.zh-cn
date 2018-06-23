---
title: 成员元素 (XMLA) |Microsoft 文档
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
- Member Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Member
- microsoft.xml.analysis.member
- http://schemas.microsoft.com/analysisservices/2003/engine#Member
helpviewer_keywords:
- Member element
ms.assetid: 5cc33a1f-192e-4821-a4ef-9a5f2bb7a9f0
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: f612e2cff38d71a956a9f273feba54cb8a867ffd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36025247"
---
# <a name="member-element-xmla"></a>Member 元素 (XMLA)
  表示单个成员的父文件夹中[成员](members-element-xmla.md)或[元组](tuple-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Members>  
   ...  
   <Member>  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </Member>  
   ...  
</Members>  
<!-- or -->  
<Tuple>  
   ...  
   <Member Hierarchy="string">  
      <UName>...</UName>  
      <Caption>...</Caption>  
      <LName>...</LName>  
      <LNum>...</LNum>  
      <DisplayInfo>...</DisplayInfo>  
   </Member>  
   ...  
</Tuple>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[成员](members-element-xmla.md)，[元组](tuple-element-xmla.md)|  
|子元素|[标题](caption-element-xmla.md)， [DisplayInfo](displayinfo-element-xmla.md)， [LName](name-element-xmla.md)， [LNum](lnum-element-xmla.md)， [UName](uname-element-xmla.md)|  
  
## <a name="attributes"></a>属性  
  
|Attribute|Description|  
|---------------|-----------------|  
|层次结构|必需的 `String` 属性（仅用于父 `Tuple` 元素）。 `Member` 元素表示的成员所属的层次结构的名称。|  
  
## <a name="remarks"></a>Remarks  
 `Member` 元素包含标识和显示给定层次结构中的成员所需的信息。 对于父 `Members` 元素，层次结构已由父元素的 `Hierarchy` 属性指定。 对于父 `Tuple` 元素，层次结构使用 `Hierarchy` 元素的 `Member` 属性来指定。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  