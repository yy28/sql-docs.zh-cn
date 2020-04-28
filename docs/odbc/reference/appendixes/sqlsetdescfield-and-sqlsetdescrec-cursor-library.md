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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b85eb84cdf48a1c2a441b8994076a9023d254f2d
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300547"
---
# <a name="sqlsetdescfield-and-sqlsetdescrec-cursor-library"></a>SQLSetDescField 和 SQLSetDescRec（游标库）
> [!IMPORTANT]  
>  此功能将在 Windows 的将来版本中删除。 避免在新的开发工作中使用此功能，并计划修改当前使用此功能的应用程序。 Microsoft 建议使用驱动程序的游标功能。  
  
 本主题讨论如何使用游标库中的**SQLSetDescField**和**SQLSetDescRec**函数。 有关这些函数的常规信息，请参阅[SQLSetDescField 函数](../../../odbc/reference/syntax/sqlsetdescfield-function.md)和[SQLSetDescRec 函数](../../../odbc/reference/syntax/sqlsetdescrec-function.md)。  
  
 当调用以返回为书签列设置的字段值时，游标库执行**SQLSetDescField** ：  
  
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
  
 对于书签列，游标库执行对**SQLSetDescRec**的调用。  
  
 当*使用 ODBC 2.x*驱动程序时，在调用**SQLSetDescField**或**SQLSetDescRec**时，游标库将返回 SQLSTATE HY090 （无效的字符串或缓冲区长度），以将 ARD 书签记录的 SQL_DESC_OCTET_LENGTH 字段设置为不等于4的值。 当*使用 ODBC 1.x*驱动程序时，游标库允许缓冲区为任意大小。  
  
 当调用 SQLSetDescField、SQL_DESC_BIND_TYPE、SQL_DESC_ROW_ARRAY_SIZE 或 SQL_DESC_ROW_STATUS_PTR 字段的 SQL_DESC_BIND_OFFSET_PTR 值时，游标库会执行**SQLSetDescField** 。 对于任何行（而不仅仅是书签行），都可以返回这些字段。  
  
 游标库不执行**SQLSetDescField**来更改除前面提到的字段之外的任何描述符字段。 如果在加载游标库时，应用程序调用**SQLSetDescField**来设置任何其他字段，则调用将传递给驱动程序。  
  
 游标库支持动态更改**SQLExtendedFetch**、 **SQLFetch**或**SQLFetchScroll**的应用程序行说明符任意行的 SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR 和 SQL_DESC_OCTET_LENGTH_PTR 字段。 只能将 SQL_DESC_OCTET_LENGTH_PTR 字段更改为 null 指针，以便取消列的长度缓冲区的绑定。  
  
 当游标打开时，游标库不支持更改 APD 或 ARD 中的 SQL_DESC_BIND_TYPE 字段。 仅在游标关闭之后以及新的游标打开之前，才能更改 SQL_DESC_BIND_TYPE 字段。 游标打开时，游标库支持更改的唯一描述符字段为 SQL_DESC_ARRAY_STATUS_PTR、SQL_DESC_BIND_OFFSET_PTR、SQL_DESC_DATA_PTR、SQL_DESC_INDICATOR_PTR、SQL_DESC_OCTET_LENGTH_PTR 和 SQL_DESC_ROWS_PROCESSED_PTR。  
  
 在调用**SQLExtendedFetch**或**SQLFetchScroll**之后以及在关闭游标之前，游标库不支持修改 ARD 的 SQL_DESC_COUNT 字段。
