---
title: StatusGraphic 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 0caf023d5405b6b97b24f733a59624d0d7dea9bd
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="statusgraphic-element-assl"></a>StatusGraphic 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含的状态的建议图形表示形式[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)元素。  
  
## <a name="syntax"></a>語法  
  
```xml  
  
<Kpi>  
   ...  
   <StatusGraphic>...</StatusGraphic>  
   ...  
</Kpi>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>備註  
 此元素的值限定为下表中列出的字符串之一。  
  
|值|Description|  
|-----------|-----------------|  
|*交通灯-单*|交通灯（单个）|  
|*交通灯-多个*|交通灯（多个）|  
|*道路标志*|路标|  
|*仪表-升序*|仪表|  
|*仪表的降序*|反向测量|  
|*温度计*|温度计|  
|*柱面*|柱状|  
|*笑脸*|脸|  
  
 对应于的父元素**StatusGraphic**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Kpi>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
