---
title: 切片元素 (ASSL) |Microsoft 文档
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
- Slice Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Slice
helpviewer_keywords:
- Slice element
ms.assetid: 2c8c4107-c641-4724-bfa5-0c47e0ec8888
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 3b1f693eddeebc0b4ad88e629eeeac9f76ca1083
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36125700"
---
# <a name="slice-element-assl"></a>Slice 元素 (ASSL)
  包含用于定义分区所含切片的多维表达式 (MDX) 表达式。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Partition>  
      ...  
   <Slice>...</Slice>  
   ...  
</Partition>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|InclusionThresholdSetting|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|分区[](../objects/partition-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Slice` 元素包含标识多维数据集中特定部分的 MDX 元组表达式或集表达式，分区将使用该部分存储信息。 MDX 表达式是类似于[StrToSet](/sql/mdx/strtoset-mdx) MDX 函数使用受约束的关键字，在表达式不能包含 MDX 或用户定义函数。  
  
 对应于的父元素`Slice`在分析管理对象 (AMO) 对象模型并<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
