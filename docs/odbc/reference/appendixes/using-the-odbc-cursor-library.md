---
title: 使用 ODBC 光标库 |微软文档
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC cursor library [ODBC], using cursor library
- cursor library [ODBC], using cursor library
ms.assetid: 9653f2f8-ccfc-4220-99ef-601dc0fa641c
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8c740ed78de51684eac38ad0c54ab2224986018d
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301398"
---
# <a name="using-the-odbc-cursor-library"></a>使用 ODBC 游标库
> [!IMPORTANT]  
>  此功能将在将来版本的 Windows 中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的光标功能。  
  
 要使用 ODBC 游标库，应用程序：  
  
1.  使用SQL_ATTR_ODBC_CURSORS*属性*调用**SQLSetConnectAttr，** 以指定如何将游标库与特定连接一起使用。 光标库始终可以使用（SQL_CUR_USE_ODBC），仅当驱动程序不支持可滚动的游标（SQL_CUR_USE_IF_NEEDED）或从未使用过（SQL_CUR_USE_DRIVER）时才使用。  
  
2.  调用**SQLConnect** **、SQLDriverConnect**或**SQLBrowseConnect**以连接到数据源。  
  
3.  调用**SQLSetStmtAttr**指定游标类型（SQL_ATTR_CURSOR_TYPE）、并发（SQL_ATTR_CONCURRENCY）和行集大小（SQL_ATTR_ROW_ARRAY_SIZE）。 游标库支持仅转发和静态游标。 仅转发游标必须是只读的，而静态游标可以是只读的，或者可以使用乐观并发控件比较值。  
  
4.  分配一个或多个行集缓冲区，并调用**SQLBindCol**一次或多次将这些缓冲区绑定到结果集列。  
  
5.  通过执行**SELECT**语句或过程或调用目录函数生成结果集。 如果应用程序将执行定位更新语句，则应执行 **"选择更新**"语句以生成结果集。  
  
6.  调用**SQLFetch**或**SQLFetch 滚动**一次或多次以滚动浏览结果集。  
  
 应用程序可以更改行集缓冲区中的数据值。 要使用光标库缓存中的数据刷新行集缓冲区，应用程序将**SQLFetchScroll 调用 SQLFetchScroll，** 其中*Fetch定向*参数设置为SQL_FETCH_RELATIVE，FetchOffset 参数设置为 0。 *FetchOffset*  
  
 若要从未绑定列检索数据，应用程序将调用**SQLSetPos**将光标定位到所需的行上。 然后调用**SQLGetData**来检索数据。  
  
 若要确定从数据源检索的行数，应用程序将调用**SQLRowCount**。
