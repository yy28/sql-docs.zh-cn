---
title: "参数化命令的操作 |Microsoft 文档"
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 65f8a1caba2f709e4583613ced4d6aa03b2d6bf1
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="operation-of-parameterized-commands"></a>参数化命令的操作
如果你正在使用大子**记录集**，尤其是与父级的大小相比**记录集**，但需访问仅在几个子的章节中，你可能会发现使用更加高效参数化的命令。  
  
 A*非参数化命令*检索整个父和子**记录集**为 parent，追加了章节列，然后将分配到每个父行的相关的子章节的引用.  
  
 A*参数化命令*检索整个父**记录集**，但仅的一章中检索**记录集**时访问的章节列。 检索策略这种差异可以产生显著的性能优势。  
  
 例如，你可以指定以下：  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 父和子表包含一个列名称常见，cust_id*。* *子命令*具有"？"占位符，RELATE 子句中引用 (即，"...参数 0"）。  
  
> [!NOTE]
>  参数子句有关仅适用于的形状命令语法。 未与任一 ADO 关联[参数](../../../ado/reference/ado-api/parameter-object.md)对象或[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。  
  
 当执行参数化的形状命令时，发生以下情况：  
  
1.  *父命令*执行并返回父**记录集**Customers 表中。  
  
2.  一个章节列追加到父级**记录集**。  
  
3.  访问父行的章节列时，*子命令*执行使用 customer.cust_id 的值作为参数的值。  
  
4.  步骤 3 中创建的数据提供程序行集中的所有行都用于填充子**记录集**。 在此示例中，这是在其中 cust_id 等于 customer.cust_id 的值订单表中的所有行。 默认情况下，子**记录集**s 将被缓存在客户端之前对父级的所有引用**记录集**发布。 若要更改此行为，设置**记录集**[动态属性](../../../ado/reference/ado-api/ado-dynamic-property-index.md)**缓存子行**到**False**。  
  
5.  检索到的子行的引用 (即，子章**记录集**) 放置在父级的当前行的章节列**记录集**。  
  
6.  访问另一个行的章节列时，将重复步骤 3 到 5。  
  
 **缓存子行**动态属性设置为**True**默认情况下。 根据查询的参数值，而不同的缓存行为。 在使用单个参数，子查询中**记录集**为给定的参数值将缓存之间具有该值的子项的请求。 下面的代码演示此：  
  
```  
SCmd = "SHAPE {select * from customer} " & _  
         "APPEND({select * from orders where cust_id = ?} " & _  
         "RELATE cust_id TO PARAMETER 0) AS chpCustOrder"  
Rst1.Open sCmd, Cnn1  
Set RstChild = Rst1("chpCustOrder").Value  
Rst1.MoveNext      ' Next cust_id passed to Param 0, & new rs fetched   
                   ' into RstChild.  
Rst1.MovePrevious  ' RstChild now holds cached rs, saving round trip.  
```  
  
 在具有两个或多个参数的查询，所有参数值与缓存的值都匹配时才使用缓存的子项。  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>参数化的命令和复杂的父子关系  
 除了使用参数化的命令来提高性能的同等联接类型层次结构，参数化的命令可用于支持更复杂的父-子关系。 例如，考虑具有两个表的少联赛数据库： 一个团队 （team_id、 团队名称） 和多个游戏 （日期、 home_team、 visiting_team） 组成。  
  
 使用非参数化的层次结构，则不能使团队和游戏表的方式相关的子**记录集**每个团队包含其完整的计划。 你可以创建包含主计划或道路计划，但不要同时的章节。 这是因为 RELATE 子句限制您的窗体的父-子关系 (pc1 = cc1) AND (pc2 = pc2)。 因此，如果你的命令包含"建立关系 team_id 收件人 home_team，team_id 收件人 visiting_team"，则将获得仅游戏团队已播放本身。 你想要的是"(team_id=home_team) 或者 (team_id = visiting_team)"，但 Shape 提供程序不支持 OR 子句。  
  
 若要获取所需的结果，可以使用参数化的命令。 例如：  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 此示例利用 SQL WHERE 子句以获取你需要的结果的更大的灵活性。  
  
> [!NOTE]
>  当 WHERE 子句，参数可以不使用 SQL 数据类型为文本、 ntext 和 image 或将产生一个错误，包含以下说明： `Invalid operator for data type`。  
  
## <a name="see-also"></a>另请参阅  
 [调整示例数据](../../../ado/guide/data/data-shaping-example.md)   
 [正式形状语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [在常规的形状命令](../../../ado/guide/data/shape-commands-in-general.md)

