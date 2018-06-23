---
title: DisplayKeyPosition 元素 (XML) |Microsoft 文档
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
ms.assetid: 345a24e6-186c-4570-baf2-7bfe9b7b4cc1
caps.latest.revision: 6
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 1f79833d15868d3e866e2a7eafd43cc352165751
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36129324"
---
# <a name="displaykeyposition-element-xml"></a>DisplayKeyPosition 元素 (XML)
  包含与元素在元素集合中的位置有关的信息。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <DisplayKeyPosition>...</DisplayKeyPosition>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Integer|  
|默认值|-1|  
|基数|0-1：出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[RelationshipEndVisualizationProperties](../../scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对于 `RelationshipEndVisualizationProperties` 元素，`DisplayKeyPosition` 元素包含显示键元素在详细信息集合中的位置。 默认值指示没有要使用的显示键。  
  
  