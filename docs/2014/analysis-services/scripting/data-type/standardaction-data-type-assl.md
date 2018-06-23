---
title: StandardAction 数据类型 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- StandardAction Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- StandardAction
helpviewer_keywords:
- StandardAction data type
ms.assetid: 81b574d5-06c1-4587-8bd2-0e5c5e3b1d99
caps.latest.revision: 37
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: bdf3282c6f75cc762ae67a9fab9fc641f25fa3a4
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36017824"
---
# <a name="standardaction-data-type-assl"></a>StandardAction 数据类型 (ASSL)
  定义一个派生的数据类型，表示任何[操作](../objects/action-element-assl.md)以外的其他元素[DrillThroughAction](action-data-type-assl.md)元素或[ReportAction](reportaction-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<StandardAction>  
   <!-- The following elements extend Action -->  
   <Expression>...</Expression>  
</StandardAction>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|[操作](action-data-type-assl.md)|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[表达式](../properties/expression-element-assl.md)|  
|派生元素|[操作](../objects/action-element-assl.md)([操作](../collections/actions-element-assl.md)集合[多维数据集](../objects/cube-element-assl.md)或[透视](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.StandardAction>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  