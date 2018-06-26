---
title: StorageLocation 元素 (ASSL) |Microsoft 文档
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
- StorageLocation Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- StorageLocation
helpviewer_keywords:
- StorageLocation element
ms.assetid: ecf8852f-56a1-4fcf-b0d8-d7eebb75e4ed
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: b6f6d023731126cafaa76cf31598e0bae9fdf1cf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36015769"
---
# <a name="storagelocation-element-assl"></a>StorageLocation 元素 (ASSL)
  包含文件系统中的父元素内容存储位置。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Cube><!-- or MeasureGroup, Partition -->  
      ...  
   <StorageLocation>...</StorageLocation>  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
|祖先或父级|默认值|  
|------------------------|-------------------|  
|[Cube](../objects/cube-element-assl.md)|InclusionThresholdSetting|  
|[度量值组](../objects/group-element-assl.md)|`StorageLocation` 父元素的 `Cube` 的值。|  
|分区[](../objects/partition-element-assl.md)|`StorageLocation` 父元素的 `MeasureGroup` 的值。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[多维数据集](../objects/cube-element-assl.md)， [MeasureGroup](../objects/group-element-assl.md)，[分区](../objects/partition-element-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对应的父级的元素`StorageLocation`分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.Cube>， <xref:Microsoft.AnalysisServices.MeasureGroup>，和<xref:Microsoft.AnalysisServices.Partition>。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;ASSL&#41;](properties-assl.md)  
  
  