---
title: PartitionID 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 88397466b303825879349caab1cd3f99353566f1
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="partitionid-element-assl"></a>PartitionID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  将相关联[分区](../../../analysis-services/scripting/objects/partition-element-assl.md)具有父元素、 绑定或外部的绑定元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<PartitionBinding>  
   ...  
   <PartitionID>...</PartitionID>  
   ...  
</PartitionBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：可出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[PartitionBinding](../../../analysis-services/scripting/data-type/partitionbinding-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 有关绑定和扩展的外部绑定的详细信息，请参阅[数据源和绑定&#40;SSAS 多维&#41;](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
