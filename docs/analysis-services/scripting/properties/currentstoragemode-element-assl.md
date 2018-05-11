---
title: CurrentStorageMode 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: b8a2b612e50b072c4b12caac321e75957ea3c952
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="currentstoragemode-element-assl"></a>CurrentStorageMode 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  确定父元素的当前存储模式。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Dimension> <!-- or Partition -->  
   <CurrentStorageMode>...</CurrentStorageMode>  
</Dimension>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|String（枚举）|  
|默认值|*ROLAP*|  
|基数|0-1：可出现一次或根本不出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[维度](../../../analysis-services/scripting/objects/dimension-element-assl.md)，[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 **CurrentStorageMode**元素指示当前正在出于主动缓存，使用的存储模式和适用于父元素的所有属性。  
  
 此元素的值限定为下表中的字符串之一。  
  
|“值”|Description|  
|-----------|-----------------|  
|*MOLAP*|父级使用多维 OLAP (MOLAP) 存储。|  
|*ROLAP*|父级使用关系 OLAP (ROLAP) 存储。|  
|*HOLAP*|父级使用混合 OLAP (HOLAP) 存储。<br /><br /> 注意： 此值才有效的[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)父元素。|  
  
 对应于允许的值在枚举**CurrentStorageMode**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.StorageMode>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
