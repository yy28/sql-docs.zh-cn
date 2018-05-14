---
title: 成员元素 (CSDLBI) |Microsoft 文档
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 39c8271c188d22cf6246e6c6c969b4a3d224b3e8
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2018
---
# <a name="member-element-csdlbi"></a>Member 元素 (CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
  
