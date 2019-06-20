---
title: 操作非参数化命令 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- non-parameterized commands [ADO]
- data shaping [ADO], non-parameterized commands
ms.assetid: 9700e50a-9f17-4ba3-8afb-f750741dc6ca
author: MightyPen
ms.author: genemi
manager: jroth
ms.openlocfilehash: 40677971cc2bc5b97c62aad1e638e52deb24c67e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "66700534"
---
# <a name="operation-of-non-parameterized-commands"></a>操作非参数化命令
对于非参数化命令，执行所有提供程序命令和**记录集**命令执行时创建。 如果该命令同步执行的所有**记录集**将完全填充。 如果选择了异步填充模式，填充的状态**记录集**将取决于填充模式和的大小**记录集**。  
  
 例如，*父命令*可能会返回**记录集**的 Customers 表，从公司的客户并*子命令*可能返回**记录集**的 Orders 表中的所有客户的订单。  
  
```  
SHAPE {SELECT * FROM Customers}   
   APPEND ({SELECT * FROM Orders} AS chapOrders   
   RELATE customerID TO customerID)  
```  
  
 对于非参数化父-子关系，每个父级和子级**记录集**对象必须具有共同点要将其关联的列。 RELATE 子句中对列的命名*父列*第一个，然后*子列*。 列可能具有不同的名称在其各自**记录集**对象而必须引用相同的信息来指定有意义的关系。 例如，**客户**并**订单记录集**对象均可以是客户 id 字段。 由于子级的成员身份**记录集**由提供程序命令，子**记录集**可以包含孤立的行。 这些孤立的行将无法访问而无需其他重新调整。  
  
 数据整理将章节列追加到父级**记录集**。 中的章节列的值是对子组织单位中的行的引用**记录集**，其中满足 RELATE 子句。 也就是说，相同的值是在*父列*给定的父行中的*子列*的一章子级的所有行。 当同一 RELATE 子句中使用多个 TO 子句时，它们是隐式组合使用 AND 运算符。 如果在 RELATE 子句中的父列不构成对父键**记录集**，单个子行可以有多个父行。  
  
 在访问中的章节列的引用时，会自动检索 ADO**记录集**表示引用。 请注意，在非参数化命令中，虽然整个子**记录集**已检索，章节只显示的行的子集。  
  
 如果没有追加的列*章别名*，它将自动生成名称。 一个[字段](../../../ado/reference/ado-api/field-object.md)列将附加到对象**记录集**对象的[字段](../../../ado/reference/ado-api/fields-collection-ado.md)集合，并且其数据类型将是**adChapter**.  
  
 了解如何浏览的分层**记录集**，请参阅[访问分层记录集的行](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)。  
  
## <a name="see-also"></a>请参阅  
 [数据整理示例](../../../ado/guide/data/data-shaping-example.md)   
 [正式 Shape 语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [常用 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
