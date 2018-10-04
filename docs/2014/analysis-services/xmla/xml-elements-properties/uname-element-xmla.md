---
title: UName 元素 (XMLA) |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- UName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#UName
- urn:schemas-microsoft-com:xml-analysis#UName
- microsoft.xml.analysis.uname
helpviewer_keywords:
- UName element
ms.assetid: b4916d44-cf77-4d4c-b4e5-a0a98192d057
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: d348fe5f1474b44df2bd765e7c9d7db2df4c809e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/02/2018
ms.locfileid: "48083617"
---
# <a name="uname-element-xmla"></a>UName 元素 (XMLA)
  包含父级的唯一名称[HierarchyInfo](hierarchyinfo-element-xmla.md)或[成员](member-element-xmla.md)元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<HierarchyInfo> <!-- or Member -->  
   ...  
   <UName>...</UName>  
   ...  
</HierarchyInfo>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|Description|  
|--------------------|-----------------|  
|数据类型和长度|String|  
|默认值|None|  
|基数|1-1：出现一次且仅出现一次的必需元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[HierarchyInfo](hierarchyinfo-element-xmla.md)，[成员](member-element-xmla.md)|  
|子元素|None|  
  
## <a name="remarks"></a>备注  
 对于 `HierarchyInfo` 元素，`UName` 元素包含可提供层次结构的唯一成员名称的属性名称。 此值等效于 OLE DB for OLAP 规范中为轴行集定义的 MEMBER_UNIQUE_NAME 属性。  
  
 对于 `Member` 元素，`UName` 元素包含父级 `Member` 元素的唯一名称。  
  
## <a name="see-also"></a>请参阅  
 [属性&#40;XMLA&#41;](xml-elements-properties.md)  
  
  
