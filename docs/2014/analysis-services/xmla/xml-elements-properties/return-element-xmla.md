---
title: 返回元素 (XMLA) |Microsoft 文档
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
- return Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.return
- http://schemas.microsoft.com/analysisservices/2003/engine#return
- urn:schemas-microsoft-com:xml-analysis#return
helpviewer_keywords:
- return element
ms.assetid: 3cfe8b74-fec3-4987-a74a-5f731444e024
caps.latest.revision: 14
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 1a4468ce3d4b14ff9cd9db7c9373083aad75d3eb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013900"
---
# <a name="return-element-xmla"></a>return 元素 (XMLA)
  包含返回的信息[DiscoverResponse](../xml-elements-objects-discoverresponse.md)到响应中的元素[发现](../xml-elements-methods-discover.md)方法调用或[ExecuteResponse](../xml-elements-objects-executeresponse.md) 到响应中的元素[执行](../xml-elements-methods-execute.md)方法调用。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DiscoverResponse> <!-- or ExecuteResponse -->  
   <return>  
      <root>...</root>  
      <!-- or -->  
      <results>...</results> <!-- ExecuteResponse only -->  
   </return>  
</DiscoverResponse>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|InclusionThresholdSetting|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DiscoverResponse](../xml-elements-objects-discoverresponse.md)， [ExecuteResponse](../xml-elements-objects-executeresponse.md)|  
|上级：[DiscoverResponse](../xml-elements-objects-discoverresponse.md)|子： <br />                        [根](root-element-xmla.md)|  
|祖先： <br />                        [ExecuteResponse](../xml-elements-objects-executeresponse.md)|子：[根](root-element-xmla.md)或[结果](results-element-xmla.md)|  
  
## <a name="remarks"></a>Remarks  
 `return` 元素包含 `Discover` 和 `Execute` 方法返回的数据。 通常，`return` 元素包含单个 `root` 元素，该元素包含由成功的 `Discover` 或 `Execute` 方法调用返回的数据，或由失败的方法调用返回的 XML for Analysis (XMLA) 异常。 如果 `Execute` 方法包含执行多个操作的 `Batch` 命令，则 `return` 元素将包含一个 `results` 元素，该元素包含所有 `root` 命令成功执行或失败执行的命令的 `Batch` 元素。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  