---
title: Resultset 数据类型 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- Resultset Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Resultset
- urn:schemas-microsoft-com:xml-analysis#Resultset
- Resultset
helpviewer_keywords:
- Resultset data type
ms.assetid: 45e7d7d6-1f89-4dc8-b39d-9270ea2db541
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a34b99aa63608faafa42d94aaf8938f86bb3894c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205475"
---
# <a name="resultset-data-type-xmla"></a>Resultset 数据类型 (XMLA)
  定义表示从返回的数据的抽象的基元数据类型[Discover](../xml-elements-methods-discover.md)或[Execute](../xml-elements-methods-execute.md)方法调用。  
  
 **Namespace** urn： 架构-microsoft-com:xml-分析： 结果集  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Resultset>  
   <Exception>...</Exception>  
   <Messages>...</Messages>  
</Resultset>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|None|  
|派生数据类型|[MDDataSet](mddataset-data-type-xmla.md)， [olapxmla_EmptyResult](emptyresult-data-type-xmla.md)，[行集](rowset-data-type-xmla.md)|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|None|  
|子元素|[异常](../xml-elements-properties/exception-element-xmla.md)，[消息](../xml-elements-properties/messages-element-xmla.md)|  
|派生元素|None|  
  
## <a name="remarks"></a>备注  
 `Resultset` 数据类型为自描述 XML 结果集，此结果集可以同时包含架构和数据，具体取决于返回的信息类型。  
  
## <a name="see-also"></a>请参阅  
 [XML 数据类型&#40;XMLA&#41;](xml-data-types-xmla.md)  
  
  
