---
title: 操作的非参数化命令 |Microsoft 文档
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- non-parameterized commands [ADO]
- data shaping [ADO], non-parameterized commands
ms.assetid: 9700e50a-9f17-4ba3-8afb-f750741dc6ca
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 3d09a577f464c5fd2e9725fcc3d475ca0360b2bf
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2018
---
# <a name="operation-of-non-parameterized-commands"></a>操作非参数化命令
非参数化命令，请执行所有提供程序命令和**记录集**命令执行过程中创建。 如果该命令以同步方式，执行所有**记录集**将完全填充。 如果选择了异步填充模式的填充的状态**记录集**将取决于的填充模式和的大小**记录集**。  
  
 例如，*父命令*可能返回**记录集**的 Customers 表，从公司的客户和*子命令*可能返回**记录集**的 Orders 表中的所有客户的订单。  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 对于非参数化父-子关系，每个父和子**记录集**对象必须具有共同点以将其关联的列。 RELATE 子句中指定了列*父列*第一个，然后*子列*。 列可能具有不同的名称在其各自**记录集**对象，但必须引用相同的信息才能指定有意义的关系。 例如，**客户**和**订单记录集**对象可能具有 customerID 字段。 因为子的成员身份**记录集**由提供程序命令，子**记录集**可以包含孤立的行。 这些孤立的行进行访问，而无需其他重新调整。  
  
 数据调整将章节列追加到父**记录集**。 中的章节列的值是对子组织单位中的行的引用**记录集**，其中满足 RELATE 子句。 相同的值，即处于*父列*给定的父行中的*子列*的章节子项的所有行。 当在相同 RELATE 子句中使用多个收件人子句时，它们将隐式组合使用 AND 运算符。 如果在 RELATE 子句中的父列不会构成父级的键**记录集**，单个子行可以有多个父行。  
  
 当访问中的章节列的引用时，会自动检索 ADO**记录集**表示引用。 请注意，在非参数化命令中，虽然整个子**记录集**已被检索，章节只显示的行的子集。  
  
 如果追加的列未包含任何*章别名*，它将自动生成名称。 A[字段](../../../ado/reference/ado-api/field-object.md)对象列将追加到**记录集**对象的[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合，并且其数据类型将**adChapter**.  
  
 有关导航分层结构信息**记录集**，请参阅[访问分层记录集中的行](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)。  
  
## <a name="see-also"></a>另请参阅  
 [调整示例数据](../../../ado/guide/data/data-shaping-example.md)   
 [正式形状语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [常用 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
