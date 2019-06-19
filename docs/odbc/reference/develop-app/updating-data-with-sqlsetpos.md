---
title: 使用 SQLSetPos 更新数据 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1c31ef622281b4f52f62ca3867c5afa7dcae8ca
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "63194413"
---
# <a name="updating-data-with-sqlsetpos"></a>使用 SQLSetPos 更新数据
应用程序可以更新或删除行集与中的任意一行**SQLSetPos**。 调用**SQLSetPos**是一个便捷替代方式构造和执行 SQL 语句。 它使 ODBC 驱动程序支持定位的更新，即使数据源不支持定位的 SQL 语句。 它是通过函数调用实现完整的数据库访问模式的一部分。  
  
 **SQLSetPos**对当前行集进行操作并在调用后才可以在**SQLFetchScroll**。 应用程序指定要更新、 删除或插入的行数和驱动程序从行集缓冲区中检索的行的新数据。 **SQLSetPos**也可用来将指定的行指定为当前行，或刷新数据源的行集中的特定行。  
  
 通过调用设置行集大小**SQLSetStmtAttr**与*属性*SQL_ATTR_ROW_ARRAY_SIZE 参数。 **SQLSetPos**使用新的行集大小，但是，仅在调用后**SQLFetch**或**SQLFetchScroll**。 例如，如果行集大小已更改， **SQLSetPos**调用，然后**SQLFetch**或**SQLFetchScroll**调用时，以及对调用**SQLSetPos**使用旧的行集大小，同时**SQLFetch**或**SQLFetchScroll**使用新的行集大小。  
  
 行集中的第一行的行编号为 1。 *RowNumber*中的参数**SQLSetPos**必须标识行集中的行; 即，其值必须介于 1 和最近提取的行数 (这可能会不会早于行集大小）。 如果*RowNumber*为 0，则该操作适用于每个行集中的行。  
  
 与关系数据库的大部分交互通过 SQL，因为**SQLSetPos**并未得到广泛支持。 但是，驱动程序可以轻松地模拟它的构造和执行**更新**或**删除**语句。  
  
 若要确定哪些操作**SQLSetPos**支持，应用程序调用**SQLGetInfo**使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、 SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、 SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 信息选项 （具体取决于游标的类型）。  
  
 本部分包含以下主题。  
  
-   [使用 SQLSetPos 更新行集中的行](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [使用 SQLSetPos 删除行集中的行](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
