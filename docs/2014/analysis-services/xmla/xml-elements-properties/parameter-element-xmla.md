---
title: Parameter 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Parameter Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Parameter
- microsoft.xml.analysis.parameter
- http://schemas.microsoft.com/analysisservices/2003/engine#Parameter
helpviewer_keywords:
- Parameter element
ms.assetid: fe31ac3d-a3e8-4f60-a81a-c43271ddbed4
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7638e033cab8f940972b35ea6c7a7a4abb402ee3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079248"
---
# <a name="parameter-element-xmla"></a>Parameter 元素 (XMLA)
  包含名称和使用的一个参数的值[Execute](../xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>语法  
  
```  
  
<Parameters>  
...  
   <Parameter>  
      <Name>...</Name>  
      <Value>...</Value>  
   </Parameter>  
...  
</Parameters>  
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
|父元素|[Parameters](parameters-element-xmla.md)|  
|子元素|[名称](name-element-parameter-xmla.md)，[值](value-element-parameter-xmla.md)|  
  
## <a name="remarks"></a>备注  
 某些 XML for Analysis (XMLA) 命令，如[进程](../xml-elements-commands/process-element-xmla.md)命令，可能需要其他信息。 `Parameter` 元素可提供一种机制，从而为 XMLA 命令提供附加信息，包括成块信息。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
