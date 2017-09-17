---
title: "操作元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Actions Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- Actions
helpviewer_keywords:
- Actions element
ms.assetid: 100a4209-2c22-4902-a8ca-f2bd99bf8fbb
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e72e49fd28d21865774b201349c48dee6b725efd
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="actions-element-assl"></a>Actions 元素 (ASSL)
  包含的操作的集合[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)或[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cube> <!-- or Perspective -->  
   ...  
   <Actions>  
      <Action xsi:type="DrillThroughAction">...</Action> <!-- ancestor: Cube -->  
      <Action xsi:type="ReportAction">...</Action> <!-- ancestor: Cube -->  
      <Action xsi:type="StandardAction">...</Action> <!-- ancestor: Cube -->  
      <!-- or -->  
      <Action xsi:type="PerspectiveAction">...</Action> <!-- ancestor: Perspective -->  
      </Actions>  
      ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无（集合）|  
|默认值|无（集合）|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)，[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)|  
|子元素|请参阅下表。|  
  
|祖先或父级|子元素|  
|------------------------|--------------------|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[DrillThroughAction](../../../analysis-services/scripting/data-type/drillthroughaction-data-type-assl.md)， [ReportAction](../../../analysis-services/scripting/data-type/reportaction-data-type-assl.md)， [StandardAction](../../../analysis-services/scripting/data-type/standardaction-data-type-assl.md)|  
|[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md)|[PerspectiveAction](../../../analysis-services/scripting/data-type/perspectiveaction-data-type-assl.md)|  
  
## <a name="remarks"></a>注释  
 在 Analysis Management Objects (AMO) 对象模型中，对应的元素为 <xref:Microsoft.AnalysisServices.ActionCollection> 和 <xref:Microsoft.AnalysisServices.PerspectiveActionCollection>。  
  
## <a name="see-also"></a>另请参阅  
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
