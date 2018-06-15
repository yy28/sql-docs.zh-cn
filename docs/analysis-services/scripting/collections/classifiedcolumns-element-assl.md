---
title: ClassifiedColumns 元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3708b343da514bfddd5fddbdf3d32b4c394b7e63
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
ms.locfileid: "34031298"
---
# <a name="classifiedcolumns-element-assl"></a>ClassifiedColumns 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含被归类的相关列的集合[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<MiningStructureColumn xsi:type="ScalarMiningStructureColumn">  
   ...  
   <ClassifiedColumns>  
      <ClassifiedColumnID>...</ClassifiedColumnID>  
   </ClassifiedColumns>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[MiningStructureColumn](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)类型的[ScalarMiningStructureColumn](../../../analysis-services/scripting/data-type/scalarminingstructurecolumn-data-type-assl.md)|  
|子元素|[ClassifiedColumnID](../../../analysis-services/scripting/properties/classifiedcolumnid-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**ClassifiedColumns**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>。  
  
## <a name="see-also"></a>另请参阅  
 [MiningStructureColumn 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)   
 [MiningStructure 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)   
 [集合 & #40;ASSL & #41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
