---
title: 关系数据类型 (ASSL) |Microsoft 文档
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
ms.assetid: 73d7c48d-d8e0-4119-849d-b5f912d449e4
caps.latest.revision: 4
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 81421605828b064644f0b9a0cfae2a7ed1b301a8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36124873"
---
# <a name="relationship-data-type-assl"></a>Relationship 数据类型 (ASSL)
  定义一个基元数据类型，该类型表示维度中的关系。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Relationship>  
   <ID>...</ID>  
   <Visible>...</Visible>  
   <FromRelationshipEnd>...</FromRelationshipEnd>  
   <ToRelationshipEnd>...</ToRelationshipEnd>  
</Relationship>  
```  
  
## <a name="data-type-characteristics"></a>数据类型特征  
  
|特征|Description|  
|--------------------|-----------------|  
|基本数据类型|InclusionThresholdSetting|  
|派生数据类型|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|InclusionThresholdSetting|  
|子元素|[ID](../properties/id-element-assl.md)，[可见](../properties/visible-element-assl.md)， [FromRelationshipEnd](relationshipend-data-type-assl.md)， [ToRelationshipEnd](relationshipend-data-type-assl.md)|  
|派生元素||  
  
## <a name="remarks"></a>Remarks  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Relationship>。  
  
## <a name="see-also"></a>请参阅  
 [Analysis Services 脚本语言 XML 数据类型&#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  