---
title: TableID 元素 (ASSL) |Microsoft 文档
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- TableID Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TableID
helpviewer_keywords:
- TableID element
ms.assetid: 45fe7e23-b274-4bc2-be63-1a5bb6680f51
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 9b8f85ee3fecac1b098a16afe6cf2d0eca61226b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36138736"
---
# <a name="tableid-element-assl"></a>TableID 元素 (ASSL)
  包含表的标识符 (ID) (从[DataSourceView](../objects/datasourceview-element-assl.md)元素) 与父元素相关联。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ColumnBinding> <!-- or DSVTableBinding, RowBinding, IncrementalProcessingNotification -->  
   ...  
   <TableID>...</TableID>  
   ...  
</ColumnBinding>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[ColumnBinding](../data-type/binding-data-type-assl.md)， [DSVTableBinding](../data-type/tablebinding-data-type-assl.md)， [IncrementalProcessingNotification](../objects/incrementalprocessingnotification-element-assl.md)， [RowBinding](../data-type/rowbinding-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 由 `TableID` 标识的表必须位于所属对象（维度或多维数据集）绑定到的数据源中。  
  
 在 Analysis Management Objects (AMO) 对象模型中，与 `TableID` 的父级对应的元素为 <xref:Microsoft.AnalysisServices.ColumnBinding>、<xref:Microsoft.AnalysisServices.DSVTableBinding>、<xref:Microsoft.AnalysisServices.IncrementalProcessingNotification> 和 <xref:Microsoft.AnalysisServices.RowBinding>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  