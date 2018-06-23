---
title: Union 函数（报表生成器和 SSRS）| Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: c87e16fe-c12a-4c9d-a9df-7a94e229fd04
caps.latest.revision: 7
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: 46d0ee10acb57e4553c176be34572fc7f6dd02d5
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/19/2018
ms.locfileid: "36024501"
---
# <a name="union-function-report-builder-and-ssrs"></a>Union 函数（报表生成器和 SSRS）
  返回在给定作用域中计算的、由表达式指定的所有非 Null 数值的联合。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## <a name="syntax"></a>语法  
  
```  
  
Union(expression, scope, recursive)  
```  
  
#### <a name="parameters"></a>Parameters  
 *expression*  
 (`SqlGeometry`或`SqlGeography`) 在其上执行聚合表达式。  
  
 *作用域*  
 (`String`) 可选。 包含要对其应用聚合函数的报表项的数据集、组或数据区域的名称。 如果未指定 *scope* ，则使用当前作用域。  
  
 *递归*  
 (**Enumerated Type**) 可选。 `Simple` （默认值） 或`RdlRecursive`。 指定是否以递归方式执行聚合。  
  
## <a name="return"></a>返回  
 返回的空间对象，或者`SqlGeometry`或`SqlGeography`、 基于表达式类型。 有关详细信息`SqlGeometry`和`SqlGeography`空间数据类型，请参阅[空间数据类型概述](../../relational-databases/spatial/spatial-data-types-overview.md)。  
  
## <a name="remarks"></a>Remarks  
 表达式中指定的数据集必须具有相同的数据类型。  
  
 *scope* 的值必须是字符串常量，不能是表达式。 对于外部聚合或未指定其他聚合的聚合， *scope* 必须引用当前作用域或包含作用域。 不支持数据集作用域。 对于聚合的聚合，嵌套聚合可以指定子作用域。  
  
 *Expression* 可以包含对嵌套聚合函数的调用，但具有以下例外和条件：  
  
-   嵌套聚合的*Scope* 必须与外部聚合的作用域相同，或者包含在外部聚合的作用域中。 对于表达式中的所有非重复作用域，一个作用域必须相对所有其他作用域处于子关系中。  
  
-   嵌套聚合的*Scope* 不能为数据集的名称。  
  
-   *表达式*不能包含`First`， `Last`， `Previous`，或`RunningValue`函数。  
  
-   *Expression* 不得包含用于指定 *recursive*的嵌套聚合。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](report-builder-functions-aggregate-functions-reference.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](expression-scope-for-totals-aggregates-and-built-in-collections.md)。  
  
 有关递归聚合的详细信息，请参阅[创建递归层次结构组（报表生成器和 SSRS）](creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## <a name="example"></a>示例  
 下表显示的示例`SqlGeometry`表达式和`Union`导致表达式，空间数据的 WKT （熟知文本） 格式中所示。  
  
|具有空间数据的字段|示例|UNION 结果|  
|-----------------------------|-------------|------------------|  
|[PointLocation]|POINT(1 2)<br /><br /> POINT(3 4)|MULTIPOINT((1 2), (3 4))|  
|[PathDefinition]|LINESTRING(1 2, 3 4)<br /><br /> LINESTRING(5 6, 7 8)|MULTILINESTRING((7 8, 5 6), (3 4, 1 2))|  
|[PolygonDefinition]|POLYGON((1 2, 3 4, 5 2, 1 2))<br /><br /> POLYGON((-1 2, -3 4, -5 2, -1 2))|MULTIPOLYGON(((1 2, 5 2, 3 4, 1 2)), ((-5 2, -1 2, -3 4, -5 2)))|  
  
```  
=Union(Fields!PointLocation.Value)  
=Union(Fields!PathDefinition.Value)  
=Union(Fields!PolygonDefinition.Value, "Group1")  
```  
  
## <a name="see-also"></a>请参阅  
 [在报表中使用表达式&#40;报表生成器和 SSRS&#41;](expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](expressions-report-builder-and-ssrs.md)   
 [总计、 聚合和内置集合的表达式作用域&#40;报表生成器和 SSRS&#41;](expression-scope-for-totals-aggregates-and-built-in-collections.md)  
  
  