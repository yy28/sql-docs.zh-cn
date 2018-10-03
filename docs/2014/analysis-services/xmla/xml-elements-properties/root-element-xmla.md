---
title: root 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Root Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#root
- urn:schemas-microsoft-com:xml-analysis#root
- microsoft.xml.analysis.root
helpviewer_keywords:
- root element
ms.assetid: ecd9d6e8-b16c-4d62-9a87-107c413a0056
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 610ef2a3b332ec59e6ddf31d7f30acfe418549e5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48110247"
---
# <a name="root-element-xmla"></a>root 元素 (XMLA)
  包含返回的结果[Discover](../xml-elements-methods-discover.md)方法或 XML for Analysis (XMLA) 命令使用执行[Execute](../xml-elements-methods-execute.md)方法。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<return> <!-- or results-->  
   ...  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:mddataset">...</root> <!-- for Execute method only -->  
   <!-- or -->  
   <root xmlns="urn:schemas-microsoft-com:xml-analysis:rowset">...</root>  
   <!-- or -->  
   <root xmlns= xmlns="urn:schemas-microsoft-com:xml-analysis:empty">...</root>  
   ...  
</return>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|默认值|None|  
|基数|1-n：可多次出现的必需元素。|  
  
## <a name="data-type-and-length"></a>数据类型和长度  
  
|Ancestor|数据类型|  
|--------------|---------------|  
|[DiscoverResponse](../xml-data-types/rowset-data-type-xmla.md)， [olapxmla_EmptyResult](../xml-data-types/emptyresult-data-type-xmla.md)|  
|[ExecuteResponse](../xml-data-types/mddataset-data-type-xmla.md)，[行集](../xml-data-types/rowset-data-type-xmla.md)， [olapxmla_EmptyResult](../xml-data-types/emptyresult-data-type-xmla.md)|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[结果](results-element-xmla.md)，[返回](return-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `root`元素包含在返回的信息[DiscoverResponse](../xml-elements-objects-discoverresponse.md)返回单个元素`Discover`方法调用中，或在[ExecuteResponse](../xml-elements-objects-executeresponse.md)元素返回的单个 XMLA 命令执行由单个`Execute`方法调用。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
