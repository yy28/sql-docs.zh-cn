---
title: AllowBrowsing 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 4737f587e17cc1a81fcb1236632869b6a4523573
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="allowbrowsing-element-assl"></a>AllowBrowsing 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  定义是否的成员[角色](../../../analysis-services/scripting/objects/role-element-assl.md)元素具有浏览权限[MiningModel](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningModelPermission>  
      ...  
   <AllowBrowsing>...</AllowBrowsing>  
   ...  
</MiningModelPermission>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|**True**|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**AllowBrowsing**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.MiningModelPermission>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
