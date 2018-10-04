---
title: Slice 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
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
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 84bcab815ec93feae3b997c0341bb8c59012cb17
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48169727"
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
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[分区](../objects/partition-element-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `Slice` 元素包含标识多维数据集中特定部分的 MDX 元组表达式或集表达式，分区将使用该部分存储信息。 MDX 表达式是类似于[StrToSet](/sql/mdx/strtoset-mdx) MDX 函数含有 CONSTRAINED 关键字，该表达式不能包含 MDX 函数或用户定义的函数。  
  
 父级对应的元素`Slice`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  
