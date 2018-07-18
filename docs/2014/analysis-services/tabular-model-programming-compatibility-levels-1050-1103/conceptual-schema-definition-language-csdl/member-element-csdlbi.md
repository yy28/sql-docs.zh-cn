---
title: Member 元素 (CSDLBI) |Microsoft Docs
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
ms.assetid: 1ba225f5-3867-4aae-a519-e3c277688d1e
caps.latest.revision: 5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4508dcf3e0dd590aaa92041d3a2136589b98e07d
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2018
ms.locfileid: "37207937"
---
# <a name="member-element-csdlbi"></a>Member 元素 (CSDLBI)
  Member 元素是一种作为其他元素的基础的复杂类型。  
  
 它的属性可能出现在列、度量值、导航属性、层次结构和级别中。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 Member 元素的元素和属性。  
  
|“属性”|是否必需|Description|  
|----------|-----------------|-----------------|  
|“属性”||向由 TMember 类型的实现所定义的成员（列、度量值、导航属性、层次结构或级别）提供的名称|  
|Caption|是|成员的显示名称。|  
|ContextualNameRule|是|用于消除成员混淆情况的命名格式。 此属性的内容由 ContextualNameRule 简单类型定义。|  
|Hidden||一个布尔值，指示是否对客户端隐藏此成员。<br /><br /> 默认值为 false，表示列在客户端中是可见的。|  
|ReferenceName||用于在 DAX 查询中引用成员的标识符。 如果忽略了此属性，则使用字段名称|  
  
## <a name="contextualnamerule-element"></a>ContextualNameRule 元素  
 此简单类型定义用于消除成员混淆情况的命名格式。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|InclusionThresholdSetting|使用属性名称。|  
|Context|使用传入关系名称。|  
|合并|连接传入的关系名称和属性名称。|  
  
## <a name="see-also"></a>请参阅  
 [了解表格对象模型](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
