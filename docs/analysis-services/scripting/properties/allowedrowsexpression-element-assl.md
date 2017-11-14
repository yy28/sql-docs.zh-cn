---
title: "AllowedRowsExpression 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: ec24b11d-d11e-4369-a619-7e41a3c46159
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: cf9c12f586ff7ffab5f627f049748d1f44eb9428
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="allowedrowsexpression-element-assl"></a>AllowedRowsExpression 元素 (ASSL)
  包含布尔类型的数据分析表达式 (DAX)，该表达式定义了父元素的内容。  
  
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
 [属性 &#40;ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

