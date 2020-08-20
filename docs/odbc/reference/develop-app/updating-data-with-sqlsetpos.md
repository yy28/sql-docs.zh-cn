---
description: 使用 SQLSetPos 更新数据
title: 用 SQLSetPos 更新数据 |Microsoft Docs
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
ms.openlocfilehash: eccc08e7af81b2b2b13dd50b2cfb0f5701174e70
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476279"
---
# <a name="updating-data-with-sqlsetpos"></a>使用 SQLSetPos 更新数据
应用程序可以通过 **SQLSetPos**更新或删除行集中的任何行。 调用 **SQLSetPos** 是构造和执行 SQL 语句的一种简便方法。 即使数据源不支持定位 SQL 语句，它也允许 ODBC 驱动程序支持定位更新。 这是通过函数调用实现数据库完全访问权限的一种模式。  
  
 **SQLSetPos** 对当前行集进行操作，并且只能在调用 **SQLFetchScroll**后使用。 应用程序指定要更新、删除或插入的行号，驱动程序从行集缓冲区中检索该行的新数据。 还可以使用**SQLSetPos**将指定行指定为当前行，或从数据源刷新行集中的特定行。  
  
 行集大小通过使用 SQL_ATTR_ROW_ARRAY_SIZE 的*属性*参数对**SQLSetStmtAttr**的调用设置。 不过， **SQLSetPos**仅在调用**SQLFetch**或**SQLFetchScroll**后使用新的行集大小。 例如，如果行集大小发生更改，则会调用 **SQLSetPos** ，然后调用 **SQLFetch** 或 **SQLFetchScroll** ，而对 **SQLSetPos** 的调用将使用旧的行集大小，而 **SQLFetch** 或 **SQLFetchScroll** 将使用新的行集大小。  
  
 行集中的第一行的行编号为 1。 **SQLSetPos**中的*RowNumber*参数必须标识行集中的行;也就是说，它的值必须介于1和最近提取的行数之间 (这可能小于行集大小) 。 如果 *RowNumber* 为0，则操作将应用于行集中的每一行。  
  
 由于与关系数据库的大多数交互是通过 SQL 来完成的，因此 **SQLSetPos** 不受广泛支持。 但是，驱动程序可以通过构造并执行 **UPDATE** 或 **DELETE** 语句来轻松地对其进行模拟。  
  
 若要确定 **SQLSetPos** 支持的操作，应用程序需要使用 SQL_DYNAMIC_CURSOR_ATTRIBUTES1、SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1、SQL_KEYSET_CURSOR_ATTRIBUTES1 或 SQL_STATIC_CURSOR_ATTRIBUTES1 信息选项调用 **SQLGetInfo** ，具体取决于游标的类型 (。  
  
 本部分包含以下主题。  
  
-   [使用 SQLSetPos 更新行集中的行](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [使用 SQLSetPos 删除行集中的行](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
