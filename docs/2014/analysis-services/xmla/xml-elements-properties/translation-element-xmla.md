---
title: Translation 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Translation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Translation
- microsoft.xml.analysis.translation
- http://schemas.microsoft.com/analysisservices/2003/engine#Translation
helpviewer_keywords:
- Translation element
ms.assetid: ce962d4b-dda9-4a16-a56c-ff7a5275c48a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7dce14aae6cd8df63d0405869b23f71874cff378
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48100457"
---
# <a name="translation-element-xmla"></a>Translation 元素 (XMLA)
  定义属性成员的翻译。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Translations>  
   ...  
   <Translation>  
      <Language>...</Language>  
      <Name>...</Name>  
   </Translation>  
   ...  
</Translations>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|None|  
|默认值|None|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[翻译](translations-element-xmla.md)|  
|子元素|[语言](language-element-xmla.md)，[名称](name-element-xmla.md)|  
  
## <a name="remarks"></a>备注  
 一个`Translation`元素定义关联属性成员与期间为给定属性定义的翻译所需的信息[插入](../xml-elements-commands/insert-element-xmla.md)或[更新](../xml-elements-commands/update-element-xmla.md)命令。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
