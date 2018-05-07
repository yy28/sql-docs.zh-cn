---
title: ForeignKeyColumn 元素 (ASSL) |Microsoft 文档
ms.date: 05/03/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1e50370a2cc4337ed797c12aaf7d7c5fe2949b2c
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/04/2018
---
# <a name="foreignkeycolumn-element-assl"></a>ForeignKeyColumn 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  标识加入关系数据源的父表的联接。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ForeignKeyColumns>  
   <ForeignKeyColumn xsi:type="DataItem">...</ForeignKeyColumn>  
</ForeignKeyColumns>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|默认值|无|  
|基数|0-n：可多次出现的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ForeignKeyColumns](../../../analysis-services/scripting/collections/foreignkeycolumns-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 有关其他信息**DataItem**类型，包括 Analysis Services 脚本语言 (ASSL) 对象和属性表**DataItem**类型，请参阅[DataItem 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)。  
  
 对应于的父元素**ForeignKeyColumns**分析管理对象 (AMO) 对象模型中的集合是<xref:Microsoft.AnalysisServices.TableMiningStructureColumn>。  
  
## <a name="see-also"></a>另请参阅  
 [TableMiningStructureColumn 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/tableminingstructurecolumn-data-type-assl.md)   
 [MiningStructureColumn 数据类型&#40;ASSL&#41;](../../../analysis-services/scripting/data-type/miningstructurecolumn-data-type-assl.md)   
 [MiningStructure 元素&#40;ASSL&#41;](../../../analysis-services/scripting/objects/miningstructure-element-assl.md)   
 [对象 & #40;ASSL & #41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  
