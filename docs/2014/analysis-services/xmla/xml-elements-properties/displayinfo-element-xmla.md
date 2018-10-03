---
title: DisplayInfo 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DisplayInfo Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- microsoft.xml.analysis.displayinfo
- http://schemas.microsoft.com/analysisservices/2003/engine#DisplayInfo
- urn:schemas-microsoft-com:xml-analysis#DisplayInfo
helpviewer_keywords:
- DisplayInfo element
ms.assetid: 059ce038-38de-4c7d-a72f-4f919cfc7c4a
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e3ff6bf5ad29ffff059752d97b03f778c5edbcf7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48101643"
---
# <a name="displayinfo-element-xmla"></a>DisplayInfo 元素 (XMLA)
  包含显示信息的父[HierarchyInfo](hierarchyinfo-element-xmla.md)或[成员](member-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <DisplayInfo>...</DisplayInfo>  
   ...  
</HierarchyInfo>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|unsignedInt|  
|默认值|None|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[HierarchyInfo](hierarchyinfo-element-xmla.md)，[成员](member-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 `DisplayInfo` 元素包含的各项信息可以帮助客户端应用程序呈现父 `HierarchyInfo` 或 `Member` 元素。 其值等效于 OLE DB for OLAP 规范中为轴行集定义的 DISPLAY_INFO 属性。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
