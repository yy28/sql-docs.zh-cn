---
title: IsDefaultImage 元素 (XML) |Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: e29cd137-af82-4753-a681-0d3e705513f3
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 0821c2dfaa25f3d9a557663046db0405aca0cb24
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48201367"
---
# <a name="isdefaultimage-element-xml"></a>IsDefaultImage 元素 (XML)
  指示可以通过将此关系导航到其他表以及提取具有属性 IsDefaultImage 的成员，获取此实体的默认图像。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<RelationshipEndVisualizationProperties>  
   ...  
   <IsDefaultImage>...</IsDefaultImage>  
   ...  
</RelationshipEndVisualizationProperties>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|Boolean|  
|默认值|false|  
|基数|0-1：出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[RelationshipEndVisualizationProperties](../../scripting/data-type/relationshipendvisualizationproperties-data-type-assl.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 对于 `RelationshipEndVisualizationProperties` 元素，`IsDefaultImage` 元素指示可通过导航到此关系的其他端，获取此实体的默认图像。 默认值 `false` 指示没有要获取的默认图像。  
  
  
