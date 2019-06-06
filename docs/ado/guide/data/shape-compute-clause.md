---
title: 形状 COMPUTE 子句 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- compute clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: 3fdfead2-b5ab-4163-9b1d-3d2143a5db8c
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: e1e268da5eb4c53b6270e474987c69b88383cd9b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66700343"
---
# <a name="shape-compute-clause"></a>Shape COMPUTE 子句
Shape COMPUTE 子句生成父级**记录集**，其列包含的引用的子**记录集**; 可选列是其内容的一章，新的或计算的列，或子级上执行聚合函数的结果**记录集**或以前成型**记录集**; 以及从子级的所有列**记录集**中列出可选的 BY 子句。  
  
## <a name="syntax"></a>语法  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>Description  
 此子句的部分如下所示：  
  
 *child-command*  
 包含以下项之一：  
  
-   在大括号内的查询命令 ("{}")，则返回一个子级**记录集**对象。 该命令颁发给基础数据提供程序，且其语法取决于该提供程序的要求。 这通常是 SQL 语言中，虽然 ADO 不需要任何特定的查询语言。  
  
-   现有的形状的名称**记录集**。  
  
-   另一个形状命令。  
  
-   表关键字后, 跟的表中的数据提供程序的名称。  
  
 *child-alias*  
 用于引用的别名**记录集**返回的*子命令。* *子别名*需要在计算子句中的列列表中，并定义父级和子级之间的关系**记录集**对象。  
  
 *appended-column-list*  
 在其中每个元素定义的生成的父代中的列列表。 每个元素包含的章节列、 一个新列、 计算的列中或从子聚合函数计算得出的值**记录集**。  
  
 *grp-field-list*  
 中的父和子列的列表**记录集**对象，指定应如何在子分组的行。  
  
 中的每列*grp 字段列表*没有的相应列中的子和父**记录集**对象。 父级中的每一行**记录集**，则*grp 字段列表*列具有唯一值和子**记录集**引用的父行只包含子它的行*grp 字段列表*列具有相同的值的父行。  
  
 如果包括，BY 子句，则子**记录集**的行分组基于计算子句中的列。 父级**记录集**将包含每个组的子组织单位中的行的一行**记录集**。  
  
 如果省略了 BY 子句，则整个子**记录集**被视为单个组和父**记录集**将包含一个行。 该行将引用整个子**记录集**。 省略 BY 子句，可对整个子计算"总计"聚合**记录集**。  
  
 例如：  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 无论采用哪种方式父级**记录集**构成 （使用计算或使用追加），它将包含用于相关的一个子级的章节列**记录集**。 如果您愿意，父级**记录集**还可能包含聚合 （SUM、 MIN、 MAX 等） 的列包含的子行。 父级和子级**记录集**可能包含在中的行的表达式中包含的列**记录集**，以及列新与最初为空。  
  
## <a name="operation"></a>操作  
 *子命令*颁发给提供程序，则返回一个子级**记录集**。  
  
 COMPUTE 子句指定的父列**记录集**，这可能是到子引用**记录集**，一个或多个聚合、 计算的表达式或新列。 如果没有 BY 子句，它定义的列还追加到父级**记录集**。 BY 子句用于指定如何的子行**记录集**进行分组。  
  
 例如，假设您有一个名为人口统计信息，其中包括状态、 城市和填充字段。 （表中的填充图提供了仅作为示例）。  
  
|State|City|人口数|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|或|Medford|200,000|  
|或|Portland|400,000|  
|CA|Los Angeles|800,000|  
|CA|San Diego|600,000|  
|WA|Tacoma|500,000|  
|或|Corvallis|300,000|  
  
 现在，发出以下形状命令：  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 此命令将打开形状**记录集**具有两个级别。 父级别是一个已生成**记录集**具有聚合的列 (`SUM(rs.population)`)、 列引用子**记录集**(`rs`)，和列进行分组子**记录集**(`state`)。 子级别**记录集**返回的查询命令 (`select * from demographics`)。  
  
 子**记录集**详细信息行进行分组的状态，但没有特定的顺序在其他情况下。 也就是说，组不会按字母或数字顺序。 如果你想父级**记录集**若要进行排序，可以使用**记录集排序**方法以对父**记录集**。  
  
 你现在可以导航打开的父**记录集**并访问子详细信息**记录集**对象。 有关详细信息，请参阅[访问分层记录集的行](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)。  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>结果的父和子详细信息记录集  
  
### <a name="parent"></a>Parent  
  
|SUM (rs。填充）|rs|State|  
|---------------------------|--------|-----------|  
|1,300,000|对 child1 引用|CA|  
|1,200,000|对 child2 引用|WA|  
|1,100,000|对 child3 引用|或|  
  
## <a name="child1"></a>Child1  
  
|State|City|人口数|  
|-----------|----------|----------------|  
|CA|Los Angeles|800,000|  
|CA|San Diego|600,000|  
  
## <a name="child2"></a>Child2  
  
|State|City|人口数|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|WA|Tacoma|500,000|  
  
## <a name="child3"></a>Child3  
  
|State|City|人口数|  
|-----------|----------|----------------|  
|或|Medford|200,000|  
|或|Portland|400,000|  
|或|Corvallis|300,000|  
  
## <a name="see-also"></a>请参阅  
 [访问分层记录集中的行](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [数据整理概述](../../../ado/guide/data/data-shaping-overview.md)   
 [字段对象](../../../ado/reference/ado-api/field-object.md)   
 [正式 Shape 语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [数据整理所需的提供程序](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Shape APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [常用 shape 命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [Value 属性 (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Visual Basic for Applications 函数](../../../ado/guide/data/visual-basic-for-applications-functions.md)
