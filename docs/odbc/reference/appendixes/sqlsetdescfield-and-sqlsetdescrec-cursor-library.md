---
title: "SQLSetDescField 和 SQLSetDescRec （光标库） |Microsoft 文档"
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
- SQLSetDescField function [ODBC], Cursor Library
- SQLSetDescRec function [ODBC], Cursor Library
ms.assetid: 4ccff067-85cd-4bfa-a6cd-7f28051fb5b9
caps.latest.revision: 9
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba3d5db821bbbfa287efb811db0ca616b01df244
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField 和 SQLSetDescRec （光标库）
> [!IMPORTANT]  
>  将 Windows 的未来版本中删除该功能。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论使用**SQLSetDescField**和**SQLSetDescRec**光标库中的函数。 有关这些函数的常规信息，请参阅[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)和[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
 游标库执行**SQLSetDescField**时调用它可返回的字段的值设置为书签列：  
  
 SQL_DESC_DATA_PTR  
  
 SQL_DESC_INDICATOR_PTR  
  
 SQL_DESC_OCTET_LENGTH_PTR  
  
 SQL_DESC_LENGTH  
  
 SQL_DESC_OCTET_LENGTH  
  
 SQL_DESC_DATETIME_INTERVAL_CODE  
  
 SQL_DESC_SCALE  
  
 SQL_DESC_PRECISION  
  
 SQL_DESC_TYPE  
  
 SQL_DESC_NAME  
  
 SQL_DESC_UNNAMED  
  
 SQL_DESC_NULLABLE  
  
 游标库执行调用**SQLSetDescRec**书签列。  
  
 当使用 ODBC 2。*x*驱动程序，光标库返回 SQLSTATE HY090 （无效字符串或缓冲区长度） 时**SQLSetDescField**或**SQLSetDescRec**调用来设置 SQL_DESC_OCTET_值不等于 4 到 ARD 的书签记录的长度字段。 使用 ODBC 3 时*.x*驱动程序，光标库允许要是任意大小的缓冲区。  
  
 游标库执行**SQLSetDescField**时调用它可返回 SQL_DESC_BIND_OFFSET_PTR、 SQL_DESC_BIND_TYPE、 SQL_DESC_ROW_ARRAY_SIZE 或 SQL_DESC_ROW_STATUS_PTR 字段的值。 对于任何行，而不仅仅是书签行，可以返回这些字段。  
  
 游标库不会执行**SQLSetDescField**更改除前面提到的字段之外的任何描述符字段。 如果应用程序调用**SQLSetDescField**要加载的是光标库时，请设置任何其他字段，请调用传递到该驱动程序。  
  
 游标库支持动态更改应用程序行描述符任何行的 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 字段 (调用了**SQLExtendedFetch**， **SQLFetch**，或**SQLFetchScroll**)。 可以将该 SQL_DESC_OCTET_LENGTH_PTR 字段更改为 null 指针只是为了取消绑定列的长度缓冲区。  
  
 游标库不支持更改 SQL_DESC_BIND_TYPE 中的字段 APD 或 ARD 打开游标时。 只有关闭光标之后，打开一个新的游标之前，可以更改 SQL_DESC_BIND_TYPE 字段。 游标库支持更改打开游标时唯一描述符字段是 SQL_DESC_ARRAY_STATUS_PTR、 SQL_DESC_BIND_OFFSET_PTR、 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR、 SQL_DESC_OCTET_LENGTH_PTR，和 SQL_DESC_ROWS_PROCESSED_PTR。  
  
 游标库不支持修改后 ARD SQL_DESC_COUNT 字段**SQLExtendedFetch**或**SQLFetchScroll**已调用和之前关闭游标。
