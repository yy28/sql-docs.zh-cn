---
title: 使用 ODBC 游标库 |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9fe19efb2d39e875cdafec76f2c50164f3a66f03
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47818425"
---
# <a name="using-the-odbc-cursor-library"></a>使用 ODBC 游标库
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 若要使用 ODBC 游标库，应用程序：  
  
1.  调用**SQLSetConnectAttr**与*属性*的 SQL_ATTR_ODBC_CURSORS，指定该游标库与特定连接的使用方式。 游标库可以始终是使用 (SQL_CUR_USE_ODBC)、 驱动程序不支持可滚动游标 (SQL_CUR_USE_IF_NEEDED) 时，才使用或从未使用过 (SQL_CUR_USE_DRIVER)。  
  
2.  调用**SQLConnect**， **SQLDriverConnect**，或**SQLBrowseConnect**连接到数据源。  
  
3.  调用**SQLSetStmtAttr**指定游标类型 (SQL_ATTR_CURSOR_TYPE)、 并发 (SQL_ATTR_CONCURRENCY) 和行集大小 (SQL_ATTR_ROW_ARRAY_SIZE)。 游标库支持只进和静态游标。 只进游标必须是只读的而静态游标可以是只读的或者可以使用乐观并发控制对值进行比较。  
  
4.  分配一个或多个行集的缓冲区并调用**SQLBindCol**一个或多个要绑定这些缓冲区以结果集列的时间。  
  
5.  生成的结果集通过执行**选择**语句或过程，或通过调用目录函数。 如果应用程序将执行定位的更新语句，则它应执行**选择更新**语句，以生成结果集。  
  
6.  调用**SQLFetch**或**SQLFetchScroll**滚动浏览结果集的一个或多个时间。  
  
 应用程序可以更改的行集缓冲区中的数据值。 若要刷新的行集缓冲区中游标库缓存的数据，应用程序调用**SQLFetchScroll**与*FetchOrientation*参数设置为 SQL_FETCH_RELATIVE 和*FetchOffset*参数设置为 0。  
  
 若要从未绑定列，应用程序调用中检索数据**SQLSetPos**将游标定位在所需的行。 然后，它调用**SQLGetData**来检索数据。  
  
 若要确定已从数据源中检索的行数，在应用程序调用**SQLRowCount**。
