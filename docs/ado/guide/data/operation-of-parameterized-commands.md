---
title: 参数化命令的操作 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- data shaping [ADO], parameterized commands
- parameterized commands [ADO]
ms.assetid: 4fae0d54-83b6-4ead-99cc-bcf532daa121
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 4001ac5b449609683293cd3174dc4410cabf4c4b
ms.sourcegitcommit: 074d44994b6e84fe4552ad4843d2ce0882b92871
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/05/2019
ms.locfileid: "66701863"
---
# <a name="operation-of-parameterized-commands"></a>参数化命令的操作
如果你正在使用较大的子**记录集**，尤其是相对于父级的大小**记录集**，但需要访问仅在几个子级的章节中，你可能会发现使用更加高效参数化的命令。  
  
 一个*非参数化命令*检索整个父和子**记录集**、 将章节列追加到父级、，然后将分配到每个父行的相关的子章节的引用.  
  
 一个*参数化命令*检索整个父**记录集**，但会检索仅章**记录集**时访问的章节列。 这种检索策略的差异可以产生显著的性能优势。  
  
 例如，可以指定以下：  
  
```  
SHAPE {SELECT * FROM customer}   
   APPEND ({SELECT * FROM orders WHERE cust_id = ?}   
   RELATE cust_id TO PARAMETER 0)  
```  
  
 父和子表具有列名称中常见，cust_id *。* *子命令*具有"？"的占位符，RELATE 子句中引用 (即，"...参数 0"）。  
  
> [!NOTE]
>  参数子句仅与形状命令语法。 未与任一 ADO 关联[参数](../../../ado/reference/ado-api/parameter-object.md)对象或[参数](../../../ado/reference/ado-api/parameters-collection-ado.md)集合。  
  
 执行参数化的形状命令时，将发生以下情况：  
  
1.  *父命令*执行，并返回父级**记录集**Customers 表中。  
  
2.  章节列追加到父级**记录集**。  
  
3.  访问父行的章节列时，*子命令*执行使用 customer.cust_id 的值作为参数的值。  
  
4.  步骤 3 中创建的数据提供程序行集中的所有行都用于填充子**记录集**。 在此示例中，这是在其中 cust_id 等于 customer.cust_id 的值订单表中的所有行。 默认情况下，子**记录集**s 将被缓存在客户端之前对父级的所有引用**记录集**发布。 若要更改此行为，请设置**记录集**[动态属性](../../../ado/reference/ado-api/ado-dynamic-property-index.md)**缓存子行**到**False**。  
  
5.  对检索到的子行的引用 (即，子的一章**记录集**) 放置在父级的当前行的章节列**记录集**。  
  
6.  访问另一行的章节列时，将重复步骤 3-5。  
  
 **缓存子行**动态属性设置为**True**默认情况下。 根据查询的参数值而不同的缓存行为。 在使用单个参数，子查询中**记录集**为给定的参数值将缓存之间具有该值的子项的请求。 下面的代码演示此：  
  
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
  
 在两个或多个参数与查询中，所有参数值与缓存的值都匹配时才使用缓存的子项。  
  
## <a name="parameterized-commands-and-complex-parent-child-relations"></a>参数化的命令和复杂的父子关系  
 除了使用参数化的命令来提高性能的同等联接类型层次结构，参数化的命令可用于支持更复杂的父-子关系。 例如，考虑具有两个表的小联盟数据库： 一个团队 （team_id、 团队名称） 和其他的游戏 （日期、 home_team、 visiting_team） 组成。  
  
 使用非参数化层次结构，没有方法相关联的方式中的团队和游戏表的子**记录集**每个团队包含其完整的计划。 您可以创建包含主计划或道路计划，但不是能同时包含的章节。 这是因为 RELATE 子句限制为窗体的父-子关系 (pc1 = cc1) 和 (pc2 = pc2)。 因此，如果您的命令包含"建立关系 team_id TO home_team，team_id TO visiting_team"，则会得到仅游戏团队已播放本身。 您需要的是"(team_id=home_team) 或者 (team_id = visiting_team)"，但 Shape 提供程序不支持 OR 子句。  
  
 若要获取所需的结果，可以使用参数化的命令。 例如：  
  
```  
SHAPE {SELECT * FROM teams}   
APPEND ({SELECT * FROM games WHERE home_team = ? OR visiting_team = ?}   
        RELATE team_id TO PARAMETER 0,   
               team_id TO PARAMETER 1)   
```  
  
 此示例中利用 SQL WHERE 子句来获取所需的结果的更大的灵活性。  
  
> [!NOTE]
>  使用 WHERE 子句，参数可以不使用 SQL 数据类型为 text、 ntext 和 image 或时，会导致错误包含以下说明： `Invalid operator for data type`。  
  
## <a name="see-also"></a>请参阅  
 [数据整理示例](../../../ado/guide/data/data-shaping-example.md)   
 [正式 Shape 语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [常用 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
