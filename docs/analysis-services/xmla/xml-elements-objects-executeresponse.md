---
title: ExecuteResponse 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 32f1994fb9205743d759fe4ae9aef294b851d26c
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="xml-elements---objects---executeresponse"></a>XML 元素的对象-ExecuteResponse
[!INCLUDE[ssas-appliesto-sqlas-aas](../../includes/ssas-appliesto-sqlas-aas.md)]
  包含返回的实例的信息[!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]以响应[执行](../../analysis-services/xmla/xml-elements-methods-execute.md)方法调用。  
  
 **Namespace** urn： 架构-microsoft-com:xml-分析  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<ExecuteResponse>  
   <return>  
</ExecuteResponse>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[返回](../../analysis-services/xmla/xml-elements-properties/return-element-xmla.md)|  
  
## <a name="remarks"></a>注释  
 **ExecuteResponse**元素是在主体中的 SOAP 响应的最顶端元素**执行**方法。  
  
## <a name="see-also"></a>另请参阅  
 [DiscoverResponse 元素&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-objects-discoverresponse.md)   
 [对象&#40;XMLA&#41;](../../analysis-services/xmla/xml-elements-objects.md)  
  
  
