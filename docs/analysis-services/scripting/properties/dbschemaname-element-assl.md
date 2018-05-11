---
title: DbSchemaName 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6ba82fbaf67e801725c87160486131b2f27cdd83
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="dbschemaname-element-assl"></a>DbSchemaName 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含使用标识的表中的父元素的架构的名称[DbTableName](../../../analysis-services/scripting/properties/dbtablename-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<TableBinding> <!-- or TableNotification -->  
   ...  
   <DbSchemaName>...</DbSchemaName>  
   ...  
</TableBinding>  
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
|父元素|[TableBinding](../../../analysis-services/scripting/data-type/tablebinding-data-type-assl.md)， [TableNotification](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应的父级的元素**DbSchemaName**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.TableBinding>和<xref:Microsoft.AnalysisServices.TableNotification>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
