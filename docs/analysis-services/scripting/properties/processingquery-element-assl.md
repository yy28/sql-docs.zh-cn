---
title: ProcessingQuery 元素 (ASSL) |Microsoft 文档
ms.date: 5/8/2018
ms.prod: sql
ms.component: assl
ms.reviewer: owend
ms.technology: analysis-services
ms.topic: reference
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 91de568e02da17298c45213ab5cdd45faf2a61f8
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="processingquery-element-assl"></a>ProcessingQuery 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含要为增量处理状态通知执行的查询的参数化文本。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<IncrementalProcessingNotification>  
   ...  
   <ProcessingQuery>...</ProcessingQuery>  
   ...  
</IncrementalProcessingNotification>  
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
|父元素|[IncrementalProcessingNotification](../../../analysis-services/scripting/objects/incrementalprocessingnotification-element-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 中的表[DataSourceView](../../../analysis-services/scripting/objects/datasourceview-element-assl.md)引用**ProcessingQuery**的同级元素，由标识[TableID](../../../analysis-services/scripting/properties/tableid-element-assl.md)。  
  
 对应于的父元素**ProcessingQuery**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.IncrementalProcessingNotification>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
