---
title: 标题元素 (XMLA) |Microsoft Docs
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
- Caption Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- urn:schemas-microsoft-com:xml-analysis#Caption
- http://schemas.microsoft.com/analysisservices/2003/engine#Caption
- microsoft.xml.analysis.caption
helpviewer_keywords:
- Caption element
ms.assetid: 3d10ee68-98ab-4da0-a409-800dea2f1c32
caps.latest.revision: 15
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 42a979937e087a1404393fe3bf4f6c6566ca5678
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37239607"
---
# <a name="caption-element-xmla"></a>Caption 元素 (XMLA)
  包含标题信息的父[HierarchyInfo](hierarchyinfo-element-xmla.md)或[成员](member-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <Caption>...</Caption>  
   ...  
</HierarchyInfo>  
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
|父元素|[HierarchyInfo](hierarchyinfo-element-xmla.md)，[成员](member-element-xmla.md)|  
|子元素|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 对于 `HierarchyInfo` 元素，`Caption` 元素包含提供层次结构的成员标题的属性名称。 其值等效于 OLE DB for OLAP 规范中为轴行集定义的 MEMBER_CAPTION 属性。  
  
 对于 `Member` 元素，`Caption` 元素包含为 XML for Analysis (XMLA) 会话指定的语言中的父 `Member` 元素的标题。 如果没有标题可用，则此元素将包含成员的唯一名称。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
