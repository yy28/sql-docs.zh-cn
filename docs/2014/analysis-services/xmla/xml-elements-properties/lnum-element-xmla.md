---
title: LNum 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- LNum Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.lnum
- urn:schemas-microsoft-com:xml-analysis#LNum
- http://schemas.microsoft.com/analysisservices/2003/engine#LNum
helpviewer_keywords:
- LNum element
ms.assetid: 7b9cc143-0c5e-4a8c-a288-8921bfcfd103
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bceb4ce6b7f54480d95f26d2c739981c2b7e299d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48210118"
---
# <a name="lnum-element-xmla"></a>LNum 元素 (XMLA)
  包含父级的级别序号位置有关的信息[HierarchyInfo](hierarchyinfo-element-xmla.md)或[成员](member-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <LNum>...</LNum>  
   ...  
</HierarchyInfo>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|ssNoversion|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[HierarchyInfo](hierarchyinfo-element-xmla.md)，[成员](member-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 对于 `HierarchyInfo` 元素，`LNum` 元素包含提供层次结构的级别序号位置的属性名称。 其值等效于 OLE DB for OLAP 规范中为轴行集定义的 LEVEL_NUMBER 属性。  
  
 有关`Member`元素，`LNum`元素包含从零开始的序号位置，从根级别的层次结构，表示父级的成员[成员](member-element-xmla.md)元素。 值零表示层次结构的根级别。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
