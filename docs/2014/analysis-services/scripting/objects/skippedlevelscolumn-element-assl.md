---
title: SkippedLevelsColumn 元素 (ASSL) |Microsoft 文档
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
- SkippedLevelsColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- SkippedLevelsColumn
helpviewer_keywords:
- SkippedLevelsColumn element
ms.assetid: 6b00a288-99c1-4735-9e6b-cd13ed4fa346
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3ae469982f39e1274759eaaea992fe456330d8fb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024425"
---
# <a name="skippedlevelscolumn-element-assl"></a>SkippedLevelsColumn 元素 (ASSL)
    
> [!NOTE]  
>  此版本的 Microsoft SQL Server 中不再使用此功能。 请避免在新的开发工作中使用该功能，并着手修改当前还在使用该功能的应用程序。  
  
 提供列的详细信息，该列存储每个成员及其父级之间跳过的（空的）级别数。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <SkippedLevelsColumn xsi:type="DataItem">...</SkippedLevelsColumn>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `SkippedLevelsColumn`元素是仅适用于父属性 (换而言之，值[用法](../properties/usage-element-dimensionattribute-assl.md)元素`DimensionAttribute`父组设置为*父*)。 `SkippedLevelsColumn` 元素包含父属性的列或属性，该列或属性存储每个成员及其父成员之间跳过的级别数。 这将允许基于父属性的父子层次结构跳过成员之间的级别。 此列或属性中包含的值必须是非负整数；否则会引发处理错误。 如果 `SkippedLevelsColumn` 元素未指定或不包含任何值，则当前成员比其父成员深一级。  
  
 有关详细信息`DataItem`类型，包括 Analysis Services 脚本语言 (ASSL) 对象和属性表`DataItem`表，请参阅[DataItem 数据类型&#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md)。  
  
 对应于的父元素`SkippedLevelsColumn`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DimensionAttribute>。  
  
## <a name="see-also"></a>请参阅  
 [属性元素&#40;ASSL&#41;](../collections/attributes-element-assl.md)   
 [维度元素&#40;ASSL&#41;](dimension-element-assl.md)   
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  