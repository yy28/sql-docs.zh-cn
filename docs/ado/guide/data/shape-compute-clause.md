---
title: "调整 COMPUTE 子句 |Microsoft 文档"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: guide
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- compute clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: 3fdfead2-b5ab-4163-9b1d-3d2143a5db8c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: d2fad39eb54af49b9f25b7f5b62073df44afc814
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="shape-compute-clause"></a>形状 COMPUTE 子句
形状 COMPUTE 子句生成父**记录集**，其列包含的参考子**记录集**; 可选其内容是章，新的或计算的列的列或子级上执行聚合函数的结果**记录集**或以前整形**记录集**; 以及从子级的任何列**记录集**中列出可选的 BY 子句。  
  
## <a name="syntax"></a>语法  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>Description  
 此子句的部分如下所示：  
  
 *子命令*  
 包括以下项之一：  
  
-   在大括号 （"{"） 中返回的查询命令**记录集**对象。 对基础数据提供程序发出该命令，其语法取决于该提供程序的要求。 通常，这是 SQL 语言中，尽管 ADO 不需要任何特定的查询语言。  
  
-   现有的形状名称**记录集**。  
  
-   另一个形状命令。  
  
-   表关键字后, 跟的表中的数据提供程序的名称。  
  
 *子别名*  
 用于引用别名**记录集**返回*子命令。* *子别名*COMPUTE 子句中的列的列表中需要并定义父级和子级之间的关系**记录集**对象。  
  
 *追加列列表*  
 在其中每个元素定义的生成的父代中的列列表。 每个元素包含一个章节列、 一个新列、 计算的列中或从子了聚合函数计算得出的值**记录集**。  
  
 *组字段列表*  
 中的父和子列的列表**记录集**指定应如何在子分组行的对象。  
  
 中的每列*组字段列表，*没有对应的列在子与父**记录集**对象。 每一行的父代中**记录集**、*组字段列表*列具有唯一值和子**记录集**引用的父行只包含子行其*组字段列表*列具有相同的值作为父行。  
  
 如果包括，了 BY 子句，则子**记录集**的行分组基于 COMPUTE 子句中的列。 父**记录集**将包含每个组的子组织单位中的行的一个行**记录集**。  
  
 如果省略了 BY 子句，则整个子**记录集**被视为单个组，父**记录集**将包含恰好一个行。 该行将引用整个子**记录集**。 省略了 BY 子句，可对整个子计算"总计"聚合**记录集**。  
  
 例如：  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 无论采用哪种方式父**记录集**构成 （使用计算或追加），它将包含用于与子级的章节列**记录集**。 如果你想，父**记录集**可能还包含子行包含聚合 （SUM、 MIN、 MAX 和等等） 的列。 父级和子级**记录集**可能包含包含在中的行的表达式中的列**记录集**，以及列新与最初为空。  
  
## <a name="operation"></a>运算  
 *子命令*颁发给提供程序，后者返回子**记录集**。  
  
 COMPUTE 子句指定的父列**记录集**，这可能会对子的引用**记录集**，一个或多个聚合、 计算的表达式或新列。 如果没有 BY 子句，它定义的列将还会追加到父**记录集**。 了 BY 子句指定如何的子行**记录集**进行分组。  
  
 例如，假定你有一个表，名为人口统计信息，其中包括状态、 市和填充字段。 （表中的填充图表是仅作为示例提供）。  
  
|State|City|人口数|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|或|Medford|200,000|  
|或|Portland|400,000|  
|CA|Los Angeles|800,000|  
|CA|圣地亚哥|600,000|  
|WA|Tacoma|500,000|  
|或|Corvallis|300,000|  
  
 现在，发出此形状命令：  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 此命令将打开特定形状**记录集**具有两个级别。 父级别是一个已生成**记录集**与聚合列 (`SUM(rs.population)`)，一个列引用子**记录集**(`rs`)，和的列进行分组子**记录集**(`state`)。 子级别是**记录集**查询命令返回 (`select * from demographics`)。  
  
 子**记录集**详细信息行进行分组的状态，但否则为顺序不分先后。 也就是说，组不会按字母或数字顺序。 如果你想父**记录集**才能进行排序; 你可以使用**记录集排序**方法进行排序父**记录集**。  
  
 你现在可以导航打开的父**记录集**访问子详细信息和**记录集**对象。 有关详细信息，请参阅[访问分层记录集中的行](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)。  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>结果父和子详细信息记录集  
  
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
|CA|圣地亚哥|600,000|  
  
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
  
## <a name="see-also"></a>另请参阅  
 [访问在分层记录集中的行](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [数据调整概述](../../../ado/guide/data/data-shaping-overview.md)   
 [字段对象](../../../ado/reference/ado-api/field-object.md)   
 [正式形状语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [记录集对象 (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [所需的提供程序，供你调整数据](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [形状 APPEND 子句](../../../ado/guide/data/shape-append-clause.md)   
 [在常规的形状命令](../../../ado/guide/data/shape-commands-in-general.md)   
 [值属性 (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Visual Basic 应用程序函数](../../../ado/guide/data/visual-basic-for-applications-functions.md)

