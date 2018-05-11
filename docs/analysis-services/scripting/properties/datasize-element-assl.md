---
title: DataSize 元素 (ASSL) |Microsoft 文档
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e6539eebfc6ba681af8c6f88faa6a381d2c4c517
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="datasize-element-assl"></a>DataSize 元素 (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  包含以字节为单位的大小[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<DataItem>  
   ...  
   <DataSize>...</DataSize>  
   ...  
</DataItem  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|子元素|无|  
  
## <a name="remarks"></a>注释  
 对应于的父元素**DataSize**在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.DataItem>。  
  
## <a name="see-also"></a>另请参阅  
 [属性 & #40;ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
