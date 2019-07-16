---
title: SQLSetDescField 和 SQLSetDescRec （游标库） |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetDescField function [ODBC], Cursor Library
- SQLSetDescRec function [ODBC], Cursor Library
ms.assetid: 4ccff067-85cd-4bfa-a6cd-7f28051fb5b9
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 5a21af2a2067498a3ec495013554b70d6a86455a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2019
ms.locfileid: "68125565"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField 和 SQLSetDescRec（游标库）
> [!IMPORTANT]  
>  此功能将 Windows 的未来版本中删除。 避免在新的开发工作中使用此功能并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题介绍如何使用**SQLSetDescField**并**SQLSetDescRec**游标库中的函数。 有关这些函数的常规信息，请参阅[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)并[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
 游标库执行**SQLSetDescField**调用返回的字段的值设置为书签列：  
  
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
  
 当使用 ODBC *2.x*驱动程序，该游标库返回 SQLSTATE HY090 （字符串或缓冲区长度无效） 时**SQLSetDescField**或**SQLSetDescRec**称为若要设置一个值为 ARD 的书签记录的 SQL_DESC_OCTET_LENGTH 字段不等于 4。 当使用 ODBC *3.x*驱动程序，该游标库允许要为任意大小的缓冲区。  
  
 游标库执行**SQLSetDescField**时被调用以返回 SQL_DESC_BIND_OFFSET_PTR、 SQL_DESC_BIND_TYPE、 SQL_DESC_ROW_ARRAY_SIZE 或 SQL_DESC_ROW_STATUS_PTR 字段的值。 对于任何行，而不仅仅是书签行，可以返回这些字段。  
  
 游标库不会执行**SQLSetDescField**更改除前面提到的字段以外的任何描述符字段。 如果应用程序调用**SQLSetDescField**若要设置的任何其他字段加载游标库时，调用将传递给驱动程序。  
  
 游标库支持动态更改的任何行的应用程序行描述符字段 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR (之后调用**SQLExtendedFetch**， **SQLFetch**，或**SQLFetchScroll**)。 可以将 SQL_DESC_OCTET_LENGTH_PTR 字段更改为 null 指针仅取消绑定的列长度的缓冲区。  
  
 游标库不支持游标打开时更改在 APD 或 ARD SQL_DESC_BIND_TYPE 字段。 可以更改 SQL_DESC_BIND_TYPE 字段，仅关闭游标之后之前打开一个新的游标。 游标库支持游标打开时更改的唯一描述符字段是 SQL_DESC_ARRAY_STATUS_PTR、 SQL_DESC_BIND_OFFSET_PTR、 SQL_DESC_DATA_PTR、 SQL_DESC_INDICATOR_PTR、 SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_ROWS_PROCESSED_PTR。  
  
 游标库不支持修改后 ARD SQL_DESC_COUNT 字段**SQLExtendedFetch**或**SQLFetchScroll**已调用之前关闭游标。
