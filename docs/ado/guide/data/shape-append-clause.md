---
title: 形状 APPEND 子句 |Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 13a91d6b8512b2c1287c3cc8e36e43a1317022d7
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062853"
---
# <a name="shape-append-clause"></a>Shape APPEND 子句
形状命令 APPEND 子句将列或列追加**记录集**。 通常情况下，这些列是章节列，请参阅子**记录集**。  
  
## <a name="syntax"></a>语法  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>Description  
 此子句的部分如下所示：  
  
 *parent-command*  
 零个或以下一项 (可以省略*父命令*完全):  
  
-   提供程序命令括在大括号 ("{}")，它返回**记录集**对象。 该命令颁发给基础数据提供程序，且其语法取决于该提供程序的要求。 这通常是 SQL 语言中，虽然 ADO 不需要任何特定的查询语言。  
  
-   另一个形状命令嵌入在括号中。  
  
-   表关键字后, 跟的表中的数据提供程序的名称。  
  
 *parent-alias*  
 指的是父级的可选别名**记录集**。  
  
 *column-list*  
 一个或多个以下：  
  
-   聚合列。  
  
-   计算的列。  
  
-   通过使用新子句创建的新列。  
  
-   章节列。 章节列的定义括在括号 （"（）"）。 请参阅下面的语法。  
  
```  
SHAPE [parent-command [[AS] parent-alias]]  
   APPEND (child-recordset [ [[AS] child-alias]   
      RELATE parent-column TO child-column | PARAMETER param-number, ... ])  
   [[AS] chapter-alias]   
   [, ... ]  
```  
  
## <a name="remarks"></a>备注  
 *child-recordset*  
 -   提供程序命令括在大括号 ("{}")，它返回**记录集**对象。 该命令颁发给基础数据提供程序，且其语法取决于该提供程序的要求。 这通常是 SQL 语言中，虽然 ADO 不需要任何特定的查询语言。  
  
-   另一个形状命令嵌入在括号中。  
  
-   现有的形状的名称**记录集**。  
  
-   表关键字后, 跟的表中的数据提供程序的名称。  
  
 *child-alias*  
 引用子级的别名**记录集**。  
  
 *parent-column*  
 中的列**记录集**返回的*父命令。*  
  
 *child-column*  
 中的列**记录集**返回的*子命令*。  
  
 *param-number*  
 请参阅[操作的参数化命令](../../../ado/guide/data/operation-of-parameterized-commands.md)。  
  
 *chapter-alias*  
 指的是附加到父级的章节列别名。  
  
> [!NOTE]
>  *"父列*TO*子列"* 子句实际上是一个列表，其中每个定义的关系用逗号分隔  
  
> [!NOTE]
>  子句后追加关键字实际上是一个列表，其中每个子句用逗号分隔，并定义要追加到父级的另一列。  
  
## <a name="remarks"></a>备注  
 在提供程序命令从用户输入构造形状命令的一部分时，形状会将用户提供的提供程序命令视为不透明的字符串和如实地将其传递给提供程序。 例如，在以下形状命令中，  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 形状将执行两个命令：`select * from t1`和 (`select * from t2 RELATE k1 TO k2)`。 如果用户提供的复合命令之间用分号分隔的多个提供程序命令组成，形状不能区分不同之处。 因此，在以下形状命令，  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 形状将执行`select * from t1; drop table t1`和 (`select * from t2 RELATE k1 TO k2),`并未意识到，`drop table t1`是单独在此示例中为危险的提供程序命令。 应用程序必须始终验证用户输入，以防止发生这种潜在的黑客攻击。  
  
 本部分包含以下主题。  
  
-   [操作非参数化命令](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [参数化命令的操作](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [混合命令](../../../ado/guide/data/hybrid-commands.md)  
  
-   [中间 Shape COMPUTE 子句](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>请参阅  
 [数据整理示例](../../../ado/guide/data/data-shaping-example.md)   
 [正式 Shape 语法](../../../ado/guide/data/formal-shape-grammar.md)   
 [常用 Shape 命令](../../../ado/guide/data/shape-commands-in-general.md)
