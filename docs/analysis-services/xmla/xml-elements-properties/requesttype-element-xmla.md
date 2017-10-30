---
title: "RequestType 元素 (XMLA) |Microsoft 文档"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- RequestType Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#RequestType
- urn:schemas-microsoft-com:xml-analysis#RequestType
- microsoft.xml.analysis.requesttype
helpviewer_keywords:
- RequestType element
ms.assetid: 54270a57-e327-4233-b4b2-d85b44652ac5
caps.latest.revision: 12
author: jeannt
ms.author: jeannt
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 88ab0c6598f57dd3971ba2b14e70dfc8ba9937c2
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="requesttype-element-xmla"></a>RequestType 元素 (XMLA)
  确定返回的元数据的类型[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)方法。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Discover>  
   ...  
   <RequestType>...</RequestType>  
   ...  
</Discover>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **RequestType**元素确定从中架构行集**发现**方法返回的数据。 此枚举仅限于支持的架构行集的名称[!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]。 有关架构行集的详细信息，请参阅[Analysis Services 架构行集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)。  
  
> [!NOTE]  
>  **RequestType**元素枚举仅架构行集名称。 如果使用架构行集 GUID，则会出错。  
  
## <a name="see-also"></a>另请参阅  
 [属性 &#40;XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  

