---
title: ErrorCode 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ErrorCode Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#ErrorCode
- microsoft.xml.analysis.errorcode
- http://schemas.microsoft.com/analysisservices/2003/engine#ErrorCode
helpviewer_keywords:
- ErrorCode element
ms.assetid: da187661-b15e-4b95-8b49-7820ebcced40
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5a86a27d9eebd0cd683bf58e0a302f1b947f9b9f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48133405"
---
# <a name="errorcode-element-xmla"></a>ErrorCode 元素 (XMLA)
  包含父级的数值返回代码[错误](error-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Error>  
   ...  
   <ErrorCode>...</ErrorCode>  
   ...  
</Error>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|UnsignedInt|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[错误](error-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
