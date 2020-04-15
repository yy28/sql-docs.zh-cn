---
title: 处理 SQL 语句 |微软文档
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
ms.openlocfilehash: 349a62034d598c1bfb44b891b91359d5ff184b7e
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280517"
---
# <a name="processing-a-sql-statement"></a>处理 SQL 语句
在讨论以编程方式使用 SQL 的技术之前，有必要讨论如何处理 SQL 语句。 所涉及的步骤是所有三种技术的共同步骤，尽管每种技术在不同时间执行它们。 下图显示了处理 SQL 语句所涉及的步骤，本节的其余部分将讨论这些步骤。  
  
 ![处理 SQL 语句的步骤](../../odbc/reference/media/pr01.gif "pr01")  
  
 要处理 SQL 语句，DBMS 执行以下五个步骤：  
  
1.  DBMS 首先分析 SQL 语句。 它将语句分解为单个单词（称为令牌），确保语句具有有效的动词和有效子句，等等。 在此步骤中可以检测到语法错误和拼写错误。  
  
2.  DBMS 验证该语句。 它根据系统目录检查语句。 语句中命名的所有表是否存在在数据库中？ 是否存在所有列，列名称是明确的？ 用户是否具有执行语句所需的权限？ 在此步骤中可以检测到某些语义错误。  
  
3.  DBMS 为语句生成访问计划。 访问计划是执行语句所需的步骤的二进制表示形式;它是等效于可执行代码的 DBMS。  
  
4.  DBMS 优化访问计划。 它探讨了执行访问计划的各种方法。 索引能否用于加快搜索速度？ DBMS 应该首先将搜索条件应用于表 A，然后将其联接到表 B，还是应该从联接开始，然后使用搜索条件？ 是否可以避免通过表进行顺序搜索，也可以缩减为表的子集？ 在探索备选方案后，DBMS 会选择其中一个。  
  
5.  DBMS 通过运行访问计划来执行语句。  
  
 用于处理 SQL 语句的步骤在所需的数据库访问量和花费的时间方面有所不同。 分析 SQL 语句不需要访问数据库，而且可以非常快速地完成。 另一方面，优化是一个非常耗费 CPU 的过程，需要访问系统目录。 对于复杂的多表查询，优化器可以探索数千种不同的执行相同查询的方法。 但是，执行查询的成本通常很高，以至于在优化中花费的时间比在提高查询执行速度中所花费的时间要高。 如果可以反复使用相同的优化访问计划来执行重复查询，则这一点更为重要。
