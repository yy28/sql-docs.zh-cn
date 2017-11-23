---
title: "处理 SQL 语句 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- sending SQL statements to DBMS [ODBC]
- SQL statements [ODBC], processing
- SQL [ODBC], processing statements
- statement processing [ODBC]
- SQL statements [ODBC]
- ODBC [ODBC], SQL
ms.assetid: 96270c4f-2efd-4dc1-a985-ed7fd5658db2
caps.latest.revision: "7"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 147d3a17b4041caf3a83ec819d65dc43af32312f
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/20/2017
---
# <a name="processing-a-sql-statement"></a>处理 SQL 语句
在讨论之前用于以编程方式使用 SQL 的技术，则需要讨论如何处理的 SQL 语句。 尽管每个方法在不同时间中执行它们，所涉及的步骤是通用的所有这三种技术。 下图演示的步骤中处理的 SQL 语句，详见本节的其余涉及。  
  
 ![用于处理 SQL 语句的步骤](../../odbc/reference/media/pr01.gif "pr01")  
  
 若要处理的 SQL 语句，DBMS，请执行以下 5 个步骤：  
  
1.  DBMS 首先分析 SQL 语句。 它划分为不同的单词，调用令牌语句，可确保语句具有一个有效的谓词和有效子句，依次类推。 在此步骤中，可以检测语法错误和拼写错误。  
  
2.  DBMS 验证该语句。 它会检查对系统目录的语句。 数据库中存在名为语句中的所有表？ 执行的所有列存在并且是否列名称明确？ 该用户是否具有所需的权限执行语句？ 在此步骤中，可以检测到某些语义错误。  
  
3.  DBMS 生成语句访问计划。 访问计划是的二进制表示形式执行语句; 所需的步骤它是可执行代码 DBMS 等效项。  
  
4.  DBMS 优化访问计划。 它探讨了各种方法来执行访问计划。 可以一起使用索引以加速搜索？ 应 DBMS 首先应用到表 A 的搜索条件，然后将它加入到表 B，或是否应以开头联接和之后使用搜索条件？ 可以通过表的顺序搜索是避免或一部分表较少？ 浏览这些替代项后, DBMS 选择其中之一。  
  
5.  DBMS 执行语句，通过运行访问计划。  
  
 用于处理 SQL 语句的步骤有所不同量它们需要的数据库访问和它们所花的时间量。 分析 SQL 语句不需要对数据库的访问，并且可以非常快速地完成。 优化，另一方面，是非常大量占用 CPU 的处理，并且需要在系统目录的访问。 对于复杂、 多表的查询，则优化器可能浏览数千个不同的方法来执行相同的查询。 但是，执行查询效率低下的成本通常是多个使用提高的查询执行速度重新获得中优化所用的时间过高的。 这是如果可以反复使用相同的优化的访问计划来执行重复性查询甚至更重要。
