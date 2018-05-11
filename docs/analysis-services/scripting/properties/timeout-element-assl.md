---
title: 超时元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 11eed8934f3831d0996b3cd41193991a8077b293
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="timeout-element-assl"></a>Timeout 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  指定以秒为单位的一段时间，这段时间之后再试图检索数据将报告超时。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataSource>  
   ...  
   <Timeout>...</Timeout>  
   ...  
</DataSource>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Duration|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataSource](../../../analysis-services/scripting/objects/datasource-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**超时**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DataSource>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
