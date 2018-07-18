---
title: AggregationFunction 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 0e465538b6528e26090f96786f98354b5253b9a7
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34032219"
---
# <a name="aggregationfunction-element-assl"></a>AggregationFunction 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含要用于帐户类型的聚合函数。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Account>  
   ...  
   <AggregationFunction>...</AggregationFunction>  
   ...  
</Account>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*Sum*|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[帐户](../../../analysis-services/scripting/objects/account-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 此元素的值限定为下列字符串之一：  
  
|“值”|Description|  
|-----------|-----------------|  
|*Sum*|度量值的聚合使用**总和**函数。|  
|*Count*|度量值的聚合使用**计数**函数。|  
|*Min*|度量值的聚合使用**Min**函数。|  
|*Max*|度量值的聚合使用**最大**函数。|  
|*DistinctCount*|度量值的聚合使用**DistinctCount**函数。|  
|*InclusionThresholdSetting*|不聚合度量值。|  
|*AverageOfChildren*|通过返回度量值子成员的平均值聚合度量值。|  
|*FirstChild*|通过返回度量值的第一个子成员聚合度量值。|  
|*LastChild*|通过返回度量值的最后一个子成员聚合度量值。|  
|*FirstNonEmpty*|通过返回度量值的第一个非空成员聚合度量值。|  
|*LastNonEmpty*|通过返回度量值的最后一个非空成员聚合度量值。|  
  
 对应于的允许值为枚举**AggregationFunction**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.AggregationFunction>。  
  
## <a name="see-also"></a>另请参阅  
 [帐户元素&#40;ASSL&#41;](../../../analysis-services/scripting/collections/accounts-element-assl.md)   
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
