---
title: 使用 SQLSetPos 更新数据 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16476a1e1007905f34ec2e70ce6032eb8d81fe7a
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286157"
---
# <a name="updating-data-with-sqlsetpos"></a>使用 SQLSetPos 更新数据
应用程序可以使用**SQLSetPos**更新或删除行集中的任何行。 调用**SQLSetPos**是构造和执行 SQL 语句的便捷替代方法。 它允许 ODBC 驱动程序支持定位更新，即使数据源不支持定位 SQL 语句也是如此。 它是通过函数调用实现完整数据库访问模式的一部分。  
  
 **SQLSetPos**在当前行集中运行，只能在调用**SQLFetchScroll**后使用。 应用程序指定要更新、删除或插入的行数，驱动程序将从行集缓冲区检索该行的新数据。 **SQLSetPos**还可用于将指定的行指定为当前行，或从数据源刷新行集中的特定行。  
  
 行集大小由对**SQLSetStmtAttr**的调用设置，*属性*参数为SQL_ATTR_ROW_ARRAY_SIZE。 但是 **，SQLSetPos**使用新的行集大小，仅在调用**SQLFetch**或**SQLFetchScroll**后。 例如，如果更改了行集大小，则调用**SQLSetPos，** 然后调用**SQLFetch**或**SQLFetchScroll，** 而**SQLSetPos 的**调用使用旧的行集大小，而**SQLFetch**或**SQLFetchScroll**使用新的行集大小。  
  
 行集中的第一行的行编号为 1。 **SQLSetPos**中的*行编号*参数必须标识行集中的行;因此，在行集中，必须标识行数。也就是说，其值必须介于 1 和最近提取的行数（可能小于行集大小）之间。 如果*RowNumber*为 0，则该操作将应用于行集中的每一行。  
  
 由于与关系数据库的大多数交互都是通过 SQL 完成的，因此**SQLSetPos**不受广泛支持。 但是，驱动程序可以通过构造和执行**UPDATE**或**DELETE**语句来轻松模拟它。  
  
 要确定**SQLSetPos**支持的操作，应用程序使用SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1或SQL_STATIC_CURSOR_ATTRIBUTES1信息选项（取决于游标的类型）调用**SQLGetInfo。**  
  
 本部分包含以下主题。  
  
-   [使用 SQLSetPos 更新行集中的行](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [使用 SQLSetPos 删除行集中的行](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
