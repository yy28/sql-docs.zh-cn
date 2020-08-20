---
description: 处理 SQL 语句
title: 处理 SQL 语句 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], processing
- SQL [ODBC], processing statements
- statement processing [ODBC]
- SQL statements [ODBC]
- ODBC [ODBC], SQL
ms.assetid: 96270c4f-2efd-4dc1-a985-ed7fd5658db2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b4ce614f6dcf4c1fe0ab1e1c806b966b4267e7fe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476214"
---
# <a name="processing-a-sql-statement"></a>处理 SQL 语句
在讨论以编程方式使用 SQL 的方法之前，必须先讨论如何处理 SQL 语句。 所有这三种方法都有所涉及的步骤，但每种方法在不同时间执行。 下图显示了处理 SQL 语句所涉及的步骤，本部分的其余部分将对此进行讨论。  
  
 ![处理 SQL 语句的步骤](../../odbc/reference/media/pr01.gif "pr01")  
  
 若要处理 SQL 语句，DBMS 需要执行以下五个步骤：  
  
1.  DBMS 首先分析 SQL 语句。 它会将语句分解为单独的单词（称为 "标记"），确保该语句具有有效的动词和有效子句等。 可在此步骤中检测语法错误和拼写错误。  
  
2.  DBMS 验证语句。 它会对照系统目录检查语句。 数据库中是否存在语句中指定的所有表？ 是否所有列都存在并且是否明确列名？ 用户是否具有执行该语句所需的权限？ 在此步骤中，可以检测到某些语义错误。  
  
3.  DBMS 为语句生成访问计划。 访问计划是执行语句所需步骤的二进制表示形式;它是可执行代码的 DBMS 等效项。  
  
4.  DBMS 优化访问计划。 它将探讨执行访问计划的各种方式。 能否使用索引来加快搜索速度？ 如果 DBMS 首先将搜索条件应用到表 A，然后将其联接到表 B，或者它是否应该以联接开头并在以后使用搜索条件？ 是否可将表中的顺序搜索避免或缩减为表的子集？ 在探索替代方法之后，DBMS 选择其中之一。  
  
5.  DBMS 通过运行访问计划来执行该语句。  
  
 用于处理 SQL 语句的步骤因所需的数据库访问量和所需的时间量而异。 分析 SQL 语句不需要对数据库的访问权限，并且可以非常快速地完成此操作。 另一方面，优化是占用大量 CPU 的进程，需要访问系统目录。 对于复杂的多表查询，优化器可能会探索数千种不同的方法来执行相同的查询。 但是，执行查询的成本效率较低，这通常是因为优化所用的时间比提高查询执行速度更多。 如果可以多次使用同一优化访问计划来执行重复的查询，则这一点更重要。
