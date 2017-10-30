---
title: "BaseProperty 元素 (CSDLBI) |Microsoft 文档"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: d0f63e52-7330-4b2c-a929-7a517acc6921
caps.latest.revision: 6
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: b82b9b6f137b09768fbfdadb78d98f9cd293e81e
ms.contentlocale: zh-cn
ms.lasthandoff: 09/01/2017

---
# <a name="baseproperty-element-csdlbi"></a>BaseProperty 元素 (CSDLBI)
  BaseProperty 元素是一种作为其他元素基础的复杂类型。  
  
 其属性可以出现在列和度量值中。  
  
## <a name="elements-and-attributes"></a>元素和属性  
 下表列出了用于定义 BaseProperty 元素的元素和属性。  
  
|名称|是否必需|Description|  
|----------|-----------------|-----------------|  
|Alignment|“否”|向由 Member 类型的实现所定义的成员（列、度量值、导航属性、层次结构或级别）提供的名称|  
|FormatString|“否”|成员的显示名称。|  
|IsRightToLeft|“否”|一个布尔值，该值指示字段是否包含可从右至左读取的文本。<br /><br /> 如果忽略此属性，则使用模型的默认设置。|  
|SortDirection|“否”|指示通常如何对字段值进行排序的一个值。 此属性的内容由 SortDirection 简单类型定义。<br /><br /> 如果省略此属性，则将基于字段的数据类型分配排序方向。|  
|单位|“否”|适用于字段值以便表示单位的符号。<br /><br /> 如果省略，则单位未知。|  
  
## <a name="alignment-element"></a>Alignment 元素  
 此简单类型定义用于消除成员混淆情况的命名格式。  
  
|“值”|Description|  
|-----------|-----------------|  
|无|使用属性名称。|  
|Context|使用传入关系名称。|  
|合并|按照当前语法的规则，将传入关系名称和属性名称串联在一起。|  
  
## <a name="sortdirection-element"></a>SortDirection 元素  
 此简单类型定义用于消除成员混淆情况的命名格式。  
  
|“值”|Description|  
|-----------|-----------------|  
|无|使用属性名称。|  
|Context|使用传入关系名称。|  
|合并|连接传入的关系名称和属性名称。|  
  
## <a name="see-also"></a>另请参阅  
 [了解表格对象模型在兼容性级别 1050年通过 1103](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  

