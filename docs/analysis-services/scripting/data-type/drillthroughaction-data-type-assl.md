---
title: "DrillThroughAction 数据类型 (ASSL) |Microsoft 文档"
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
- DrillThroughAction Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- DrillThroughAction
helpviewer_keywords:
- DrillThroughAction data type
ms.assetid: e212d575-a0d7-4548-92b4-33542ef59034
caps.latest.revision: 38
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8859e7c9187bdbb491d3e67c812268e648aa1173
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="drillthroughaction-data-type-assl"></a>DrillThroughAction 数据类型 (ASSL)
  定义表示钻取操作的派生数据类型。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DrillThroughAction>  
   <!-- The following elements extend Action -->  
   <Default>...</Default>  
   <Columns>...</Columns>  
</DrillThroughAction>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|[操作](../../../analysis-services/scripting/data-type/action-data-type-assl.md)|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[列](../../../analysis-services/scripting/collections/columns-element-assl.md)，[默认](../../../analysis-services/scripting/properties/default-element-assl.md)|  
|派生元素|[操作](../../../analysis-services/scripting/objects/action-element-assl.md)([操作](../../../analysis-services/scripting/collections/actions-element-assl.md)，集合[多维数据集](../../../analysis-services/scripting/objects/cube-element-assl.md)，或[透视](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.DrillThroughAction>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

