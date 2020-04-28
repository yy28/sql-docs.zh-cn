---
title: Long Data 和 SQLSetPos 和 SQLBulkOperations |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4bc6c5d2da2f796a7c312971635fc36bc2fae8af
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2020
ms.locfileid: "81287861"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Long 数据和 SQLSetPos 及 SQLBulkOperations
与 SQL 语句中的参数一样，在通过**SQLBulkOperations**或**SQLSetPos**更新行或在通过**SQLBulkOperations**插入行时，可以发送长数据。 数据在部分中发送，多个调用**SQLPutData**。 在执行时发送数据的列称为 "*执行时数据" 列*。  
  
> [!NOTE]  
>  尽管只能在部分中发送字符和二进制数据，但应用程序实际上可以使用**SQLPutData**在执行时发送任意类型的数据。 但是，如果数据太小，足以容纳在单个缓冲区中，通常没有理由使用**SQLPutData**。 绑定缓冲区并让驱动程序从缓冲区中检索数据，这要简单得多。  
  
 由于长数据列通常未绑定，因此应用程序必须先绑定列，然后再调用**SQLBulkOperations**或**SQLSetPos** ，然后在调用**SQLBulkOperations**或**SQLSetPos**后将其解除绑定。 必须绑定列，因为**SQLBulkOperations**或**SQLSetPos**仅对绑定列运行，并且必须解除绑定，以便可以使用**SQLGetData**来从列中检索数据。  
  
 若要在执行时发送数据，应用程序需要执行以下操作：  
  
1.  将32位值置于行集缓冲区中，而不是数据值。 此值稍后将返回到应用程序，因此应用程序应将其设置为有意义的值，如列号或包含数据的文件的句柄。  
  
2.  将长度/指示器缓冲区中的值设置为 SQL_LEN_DATA_AT_EXEC （*长度*）宏的结果。 此值向驱动程序指示参数的数据将与**SQLPutData**一起发送。 当向数据源发送长数据时，将使用*长度*值，该数据源需要知道将发送多少字节的长数据以便它能够预分配空间。 若要确定数据源是否需要此值，应用程序需要使用 SQL_NEED_LONG_DATA_LEN 选项调用**SQLGetInfo** 。 所有驱动程序都必须支持此宏;如果数据源不需要字节长度，则驱动程序可以忽略此长度。  
  
3.  调用**SQLBulkOperations**或**SQLSetPos**。 驱动程序发现长度/指示器缓冲区包含 SQL_LEN_DATA_AT_EXEC （*长度*）宏的结果，并将 SQL_NEED_DATA 作为函数的返回值返回。  
  
4.  调用**SQLParamData**以响应 SQL_NEED_DATA 返回值。 如果需要发送长数据， **SQLParamData**返回 SQL_NEED_DATA。 在由*ValuePtrPtr*参数指向的缓冲区中，驱动程序将返回应用程序置于行集缓冲区中的唯一值。 如果有多个执行时数据列，应用程序将使用此值来确定要为其发送数据的列;此驱动程序不要求以任何特定顺序请求执行时数据列的数据。  
  
5.  调用**SQLPutData**将列数据发送给驱动程序。 如果列数据不能放在单个缓冲区中，通常情况下，长数据的情况下，应用程序将重复调用**SQLPutData**以在部分中发送数据;驱动程序和数据源由驱动程序和数据源组成，用于重组数据。 如果应用程序传递了以 null 结尾的字符串数据，则驱动程序或数据源必须删除 null 终止字符作为重汇编过程的一部分。  
  
6.  再次调用**SQLParamData** ，以指示它已发送列的所有数据。 如果数据尚未发送到任何执行时数据列，驱动程序将返回 SQL_NEED_DATA，并为下一次执行时数据列返回唯一值;应用程序返回到步骤5。 如果已为所有执行时数据列发送了数据，则行的数据将发送到数据源。 然后， **SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，可以返回**SQLBulkOperations**或**SQLSETPOS**可以返回的任何 SQLSTATE。  
  
 在**SQLBulkOperations**或**SQLSetPos**返回 SQL_NEED_DATA 之后，在为最后一个执行时数据列完全发送数据之前，该语句处于需要数据状态。 在此状态下，应用程序只能调用**SQLPutData**、 **SQLParamData**、 **SQLCancel**、 **SQLGetDiagField**或**SQLGetDiagRec**;所有其他函数返回 SQLSTATE HY010 （函数序列错误）。 调用**SQLCancel**将取消语句的执行，并将其返回到它以前的状态。 有关详细信息，请参阅[附录 B： ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
