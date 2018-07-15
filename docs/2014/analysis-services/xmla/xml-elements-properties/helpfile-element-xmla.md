---
title: HelpFile 元素 (XMLA) |Microsoft Docs
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
- HelpFile Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#HelpFile
- http://schemas.microsoft.com/analysisservices/2003/engine#HelpFile
- microsoft.xml.analysis.helpfile
helpviewer_keywords:
- HelpFile element
ms.assetid: 537ea7a8-5064-4a31-b0cd-ab7e891fef09
caps.latest.revision: 10
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6ccf47f3e47e6521dd9c3909b71315ae4d9768de
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37195977"
---
# <a name="helpfile-element-xmla"></a>HelpFile 元素 (XMLA)
  包含到介绍父主题的帮助文件的路径或 URL[错误](error-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Error>  
   ...  
   <HelpFile>...</HelpFile>  
   ...  
</Error>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[错误](error-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
