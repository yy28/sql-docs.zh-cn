---
title: CurrentTimeMember 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0f43b181e6e827f2b012f7c814d0de6f489a5564
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="currenttimemember-element-assl"></a>CurrentTimeMember 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义与维度关联的时间的当前成员[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Kpi>  
   ...  
   <CurrentTimeMember>...</CurrentTimeMember>  
   ...  
</AggregationDimension>  
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
  
## <a name="remarks"></a>注释  
 此元素的值是计算结果为时间维度中单个成员的多维表达式 (MDX) 语句，用于检索计算关键绩效指标 (KPI) 时的当前时间范围。  
  
 对应于的父元素**CurrentTimeMember**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Kpi>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
