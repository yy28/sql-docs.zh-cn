---
title: "关系数据类型 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 73d7c48d-d8e0-4119-849d-b5f912d449e4
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: adf9322bebc1e1ed33af880fd435cddcde5293c1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

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
  
|特征|说明|  
|--------------------|-----------------|  
|基本数据类型|无|  
|派生数据类型|无|  
  
## <a name="data-type-relationships"></a>数据类型关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|无|  
|子元素|[ID](../../../analysis-services/scripting/properties/id-element-assl.md)，[可见](../../../analysis-services/scripting/properties/visible-element-assl.md)， [FromRelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md)， [ToRelationshipEnd](../../../analysis-services/scripting/data-type/relationshipend-data-type-assl.md)|  
|派生元素||  
  
## <a name="remarks"></a>注释  
 分析管理对象 (AMO) 对象模型中的相应元素是<xref:Microsoft.AnalysisServices.Relationship>。  
  
## <a name="see-also"></a>另请参阅  
 [Analysis Services 脚本语言 XML 数据类型 &#40;ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  

