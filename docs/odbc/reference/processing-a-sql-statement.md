---
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: edf912bf3b8073a05dd900cd00511715020ee0c2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808985"
---
# <a name="processing-a-sql-statement"></a>处理 SQL 语句
在讨论之前用于以编程方式使用 SQL 的技术，有必要讨论如何处理 SQL 语句。 尽管每种技术在不同时间执行它们所涉及的步骤是普遍适用于所有这三种技术。 下图显示所涉及步骤中处理 SQL 语句，对此进行讨论本部分的其余部分。  
  
 ![处理 SQL 语句的步骤](../../odbc/reference/media/pr01.gif "pr01")  
  
 若要处理的 SQL 语句，DBMS，请执行以下五个步骤：  
  
1.  DBMS 将首先分析 SQL 语句。 该语句分解成不同的单词，名为令牌，可确保语句具有一个有效的谓词和有效子句，等等。 在此步骤中，可以检测语法错误和拼写错误。  
  
2.  DBMS 验证该语句。 它会检查对系统目录的语句。 不要在数据库中存在名为语句中的所有表？ 执行操作的所有列存在并且是明确的列名称？ 该用户是否具有所需的权限，无法执行该语句？ 在此步骤中，可以检测到某些语义错误。  
  
3.  DBMS 生成语句访问计划。 访问计划是二进制表示形式的语句; 执行所需的步骤它相当于 DBMS 的可执行代码。  
  
4.  DBMS 优化访问计划。 它探讨了各种方法来执行访问计划。 可索引用于搜索的速度？ 应 DBMS 第一次将搜索条件应用到表 A，然后将其加入到表 B 或应开头联接，然后使用搜索条件？ 可以通过一个表的顺序搜索避免或减少到的表的子集？ 浏览备选项之后, DBMS 选择其中之一。  
  
5.  DBMS 的运行访问计划来执行该语句。  
  
 用于处理 SQL 语句的步骤有所不同量所需的数据库访问和所采用的时间量。 分析 SQL 语句不需要对数据库的访问，并且可以非常快速地完成。 优化后，就是大量占用 CPU 的处理，并要求对系统目录的访问。 有关复杂多表的查询优化器可能浏览数千个不同的方法来执行相同的查询。 但是，查询执行效率低下的成本通常是如此之高优化所用的时间超过了增加的查询执行速度重新获得的。 这是更大，如果可以反复使用相同的优化的访问计划来执行重复的查询。
