---
title: 表达式元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: a58830744e205ab46d5e326ec17d00c6faab3dd6
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="expression-element-assl"></a>Expression 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含定义父元素内容的多维表达式 (MDX)。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<CellPermission> <!-- or StandardAction -->  
   ...  
   <Expression>...</Expression>  
   ...  
</CellPermission>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|字符串|  
|默认值|无|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[CellPermission](../../../analysis-services/scripting/objects/cellpermission-element-assl.md)， [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 有关**CellPermission**元素，**表达式**元素包含一个逻辑的 MDX 表达式，标识适用于由的权限的单元格[访问](../../../analysis-services/scripting/properties/access-element-assl.md)元素的**CellPermission**元素。 如果值**表达式**元素**CellPermission**元素为空， **CellPermission**元素将被忽略。  
  
 有关**StandardAction**元素，**表达式**元素包含一个表示操作的内容的 MDX 表达式。 如果值**表达式**元素**StandardAction**元素为空， **StandardAction**元素将被忽略。  
  
 在 Analysis Management Objects (AMO) 对象模型中，与父级对应的元素为 <xref:Microsoft.AnalysisServices.CellPermission> 和 <xref:Microsoft.AnalysisServices.StandardAction>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
