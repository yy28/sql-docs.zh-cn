---
title: TableID 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 64368ed911696ae67d6d72e5b02951ffad113967
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="tableid-element-assl"></a>TableID 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含表的标识符 (ID) (从[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)元素) 与父元素相关联。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<ColumnBinding> <!-- or DSVTableBinding, RowBinding, IncrementalProcessingNotification -->  
   ...  
   <TableID>...</TableID>  
   ...  
</ColumnBinding>  
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
|父元素|[ColumnBinding](../../../analysis-services/scripting/data-type/columnbinding-data-type-assl.md)， [DSVTableBinding](../../../analysis-services/scripting/data-type/dsvtablebinding-data-type-assl.md)， [IncrementalProcessingNotification](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md)， [RowBinding](../../../analysis-services/scripting/data-type/rowbinding-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 标识的表**TableID**必须所属的对象 （维度或多维数据集） 绑定到的数据源中。  
  
 对应的父级的元素**TableID**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.ColumnBinding>， <xref:Microsoft.AnalysisServices.DSVTableBinding>， <xref:Microsoft.AnalysisServices.IncrementalProcessingNotification>，和<xref:Microsoft.AnalysisServices.RowBinding>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
