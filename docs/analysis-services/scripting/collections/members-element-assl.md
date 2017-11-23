---
title: "Members 元素 (ASSL) |Microsoft 文档"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Members Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Members
helpviewer_keywords: Members element
ms.assetid: 4bf585a3-b681-486d-852b-1244c5658a04
caps.latest.revision: "34"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8b7a4a67e738d500661a430a1fb55a93284c50e8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="members-element-assl"></a>Members 元素 (ASSL)
  包含的集合[成员](../../../analysis-services/scripting/objects/member-element-assl.md)父元素的元素。  
  
## <a name="syntax"></a>语法  
  
```xml  
  
<Group> <!-- or Role --<  
   ...  
   <Members>  
      <Member>...</Member>  
   </Members>  
   ...  
</Group>  
```  
  
## <a name="element-characteristics"></a>元素特征  
  
|特征|说明|  
|--------------------|-----------------|  
|数据类型和长度|无|  
|默认值|无|  
|基数|0-1：可出现一次且仅出现一次的可选元素。|  
  
## <a name="element-relationships"></a>元素关系  
  
|关系|元素|  
|------------------|-------------|  
|父元素|[组](../../../analysis-services/scripting/objects/group-element-assl.md)，[角色](../../../analysis-services/scripting/objects/role-element-assl.md)|  
|子元素|[成员](../../../analysis-services/scripting/objects/member-element-assl.md)|  
  
## <a name="remarks"></a>注释  
 对应的父级的元素**成员**分析管理对象 (AMO) 对象模型中是<xref:Microsoft.AnalysisServices.Group>和<xref:Microsoft.AnalysisServices.Role>。  
  
## <a name="see-also"></a>另请参阅  
 [集合 &#40;ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
