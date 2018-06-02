---
title: RequestType 元素 (XMLA) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 63c1a838d74745b5ef51f73b51e34c95e08a81ff
ms.sourcegitcommit: 808d23a654ef03ea16db1aa23edab496b73e5072
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2018
ms.locfileid: "34577619"
---
# <a name="requesttype-element-xmla"></a>RequestType 元素 (XMLA)
[!INCLUDE[ssas-appliesto-sqlas-aas](../../../includes/ssas-appliesto-sqlas-aas.md)]
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
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[发现](../../../analysis-services/xmla/xml-elements-methods-discover.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 **RequestType**元素确定从中架构行集**发现**方法返回的数据。 此枚举仅限于 Analysis Services 支持的架构行集的名称。 有关架构行集的详细信息，请参阅[Analysis Services 架构行集](../../../analysis-services/schema-rowsets/analysis-services-schema-rowsets.md)。  
  
> [!NOTE]  
>  **RequestType**元素枚举仅架构行集名称。 如果使用架构行集 GUID，则会出错。  
  
## <a name="see-also"></a>另请参阅
 [属性&#40;XMLA&#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  
