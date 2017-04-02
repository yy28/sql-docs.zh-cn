---
title: "Union 函数（报表生成器和 SSRS） | Microsoft Docs"
ms.custom: ""
ms.date: "12/09/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c87e16fe-c12a-4c9d-a9df-7a94e229fd04
caps.latest.revision: 7
author: "maggiesMSFT"
ms.author: "maggies"
manager: "erikre"
---
# Union 函数（报表生成器和 SSRS）
  返回在给定作用域中计算的、由表达式指定的所有非 Null 数值的联合。  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
## 语法  
  
```  
  
Union(expression, scope, recursive)  
```  
  
#### Parameters  
 *expression*  
 （**SqlGeometry** 或 **SqlGeography**）要对其执行聚合的表达式。  
  
 *作用域*  
 (**String**) 可选。 包含要对其应用聚合函数的报表项的数据集、组或数据区域的名称。 如果未指定 *scope* ，则使用当前作用域。  
  
 *递归*  
 (**Enumerated Type**) 可选。 **Simple**（默认）或 **RdlRecursive**。 指定是否以递归方式执行聚合。  
  
## 返回  
 返回一个空间对象 **SqlGeometry** 或 **SqlGeography**，具体取决于表达式类型。 有关 **SqlGeometry** 和 **SqlGeography** 空间数据类型的详细信息，请参阅[空间数据类型概述](../../relational-databases/spatial/spatial-data-types-overview.md)。  
  
## 注释  
 表达式中指定的数据集必须具有相同的数据类型。  
  
 *scope* 的值必须是字符串常量，不能是表达式。 对于外部聚合或未指定其他聚合的聚合， *scope* 必须引用当前作用域或包含作用域。 不支持数据集作用域。 对于聚合的聚合，嵌套聚合可以指定子作用域。  
  
 *Expression* 可以包含对嵌套聚合函数的调用，但具有以下例外和条件：  
  
-   嵌套聚合的*Scope* 必须与外部聚合的作用域相同，或者包含在外部聚合的作用域中。 对于表达式中的所有非重复作用域，一个作用域必须相对所有其他作用域处于子关系中。  
  
-   嵌套聚合的*Scope* 不能为数据集的名称。  
  
-   *Expression* 不得包含 **First**、 **Last**、 **Previous**或 **RunningValue** 函数。  
  
-   *Expression* 不得包含用于指定 *recursive*的嵌套聚合。  
  
 有关详细信息，请参阅[聚合函数引用（报表生成器和 SSRS）](../../reporting-services/report-design/aggregate-functions-reference-report-builder-and-ssrs.md)和[总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md)。  
  
 有关递归聚合的详细信息，请参阅[创建递归层次结构组（报表生成器和 SSRS）](../../reporting-services/report-design/creating-recursive-hierarchy-groups-report-builder-and-ssrs.md)。  
  
## 示例  
 下表说明 **SqlGeometry** 表达式和 **Union** 结果表达式的示例，它们以空间数据的 WKT（熟知文本）格式显示。  
  
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
  
## 另请参阅  
 [在报表中使用表达式（报表生成器和 SSRS）](../../reporting-services/report-design/expression-uses-in-reports-report-builder-and-ssrs.md)   
 [表达式示例（报表生成器和 SSRS）](../../reporting-services/report-design/expression-examples-report-builder-and-ssrs.md)   
 [表达式中的数据类型（报表生成器和 SSRS）](../../reporting-services/report-design/data-types-in-expressions-report-builder-and-ssrs.md)   
 [总计、聚合和内置集合的表达式作用域（报表生成器和 SSRS）](../../reporting-services/report-design/expression scope for totals, aggregates, and built-in collections.md)  
  
  