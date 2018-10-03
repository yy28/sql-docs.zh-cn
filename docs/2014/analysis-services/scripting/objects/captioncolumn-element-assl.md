---
title: CaptionColumn 元素 (ASSL) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- CaptionColumn Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CaptionColumn
helpviewer_keywords:
- CaptionColumn element
ms.assetid: bdb1b9b8-b5d5-4d91-81c7-8de8635bbb83
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bc8f782456b47f03ca8a7eab1bf9407020fda3f3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48108987"
---
# <a name="captioncolumn-element-assl"></a>CaptionColumn 元素 (ASSL)
  定义提供属性标题的列。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<AttributeTranslation>  
   ...  
   <CaptionColumn xsi:type="DataItem">...</CaptionColumn>  
   ...  
</AttributeTranslation>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[AttributeTranslation](../data-type/translation-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 有关详细信息`DataItem`类型，包括 Analysis Services 脚本语言 (ASSL) 对象和属性表`DataItem`类型，请参阅[DataItem 数据类型&#40;ASSL&#41;](../data-type/dataitem-data-type-assl.md)。  
  
 父级对应的元素`CaptionColumn`在 Analysis Management Objects (AMO) 对象模型是<xref:Microsoft.AnalysisServices.AttributeTranslation>。  
  
## <a name="see-also"></a>请参阅  
 [对象&#40;ASSL&#41;](objects-assl.md)  
  
  
