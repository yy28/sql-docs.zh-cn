---
title: "成员元素 (CSDLBI) |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
ms.assetid: 1ba225f5-3867-4aae-a519-e3c277688d1e
caps.latest.revision: "6"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: a97b171f1205b2718b5786ae92fce826c2c6316c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/17/2017
---
# <a name="member-element-csdlbi"></a>Member 元素 (CSDLBI)
  Member 元素是一种作为其他元素的基础的复杂类型。  
  
 它的属性可能出现在列、度量值、导航属性、层次结构和级别中。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 Member 元素的元素和属性。  
  
|名称|是否必需|Description|  
|----------|-----------------|-----------------|  
|名称||向由 TMember 类型的实现所定义的成员（列、度量值、导航属性、层次结构或级别）提供的名称|  
|Caption|是|成员的显示名称。|  
|ContextualNameRule|是|用于消除成员混淆情况的命名格式。 此属性的内容由 ContextualNameRule 简单类型定义。|  
|Hidden||一个布尔值，指示是否对客户端隐藏此成员。<br /><br /> 默认值为 false，表示列在客户端中是可见的。|  
|ReferenceName||用于在 DAX 查询中引用成员的标识符。 如果忽略了此属性，则使用字段名称|  
  
## <a name="contextualnamerule-element"></a>ContextualNameRule 元素  
 此简单类型定义用于消除成员混淆情况的命名格式。  
  
|“值”|Description|  
|-----------|-----------------|  
|无|使用属性名称。|  
|Context|使用传入关系名称。|  
|合并|连接传入的关系名称和属性名称。|  
  
## <a name="see-also"></a>另请参阅  
 [了解表格对象模型在兼容性级别 1050年通过 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  
