---
title: "使用 SQLSetPos 更新数据 |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: fb89d4a2220c487f2e126b50ecf8cbedd20857cc
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="updating-data-with-sqlsetpos"></a>使用 SQLSetPos 更新数据
应用程序可以更新或删除任何行集中的行与**SQLSetPos**。 调用**SQLSetPos**是一个便捷替代方式构造和执行 SQL 语句。 它可让 ODBC 驱动程序支持定位的更新，即使数据源不支持定位的 SQL 语句。 它是范例的通过函数调用实现完整的数据库访问的一部分。  
  
 **SQLSetPos**当前行集上运行并在调用后才可以使用**SQLFetchScroll**。 应用程序指定要更新、 删除或插入的行数和驱动程序从行集缓冲区检索该行的新数据。 **SQLSetPos**还可将指定的行指定为当前行中，或刷新特定行集中的数据源的行。  
  
 通过调用设置行集大小**SQLSetStmtAttr**与*属性*SQL_ATTR_ROW_ARRAY_SIZE 自变量。 **SQLSetPos**使用行集大小的最新的但是，仅在调用后**SQLFetch**或**SQLFetchScroll**。 例如，如果更改的行集大小， **SQLSetPos**调用，然后**SQLFetch**或**SQLFetchScroll**调用时，和对**SQLSetPos**使用旧的行集大小时**SQLFetch**或**SQLFetchScroll**使用新的行集大小。  
  
 行集中的第一行的行编号为 1。 *RowNumber*中的参数**SQLSetPos**必须标识行集中的行; 即，其值必须介于 1 和最近提取的行数 (这可能会早于行集大小）。 如果*RowNumber*为 0，则该操作适用于每个行集中的行。  
  
 因为大多数与关系数据库的交互通过 SQL， **SQLSetPos**不受广泛支持。 但是，驱动程序可以轻松地模拟它方法是构造并执行**更新**或**删除**语句。  
  
 若要确定哪些操作**SQLSetPos**支持的功能，应用程序调用**SQLGetInfo**使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 信息选项 （具体取决于游标的类型）。  
  
 本部分包含以下主题。  
  
-   [使用 SQLSetPos 更新的行集中的行](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [删除与 SQLSetPos 行集中的行](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
