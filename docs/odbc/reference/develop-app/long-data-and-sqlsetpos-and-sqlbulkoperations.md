---
title: 长数据和 SQLSetPos 和 SQLBulk 操作 |微软文档
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287861"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Long 数据和 SQLSetPos 及 SQLBulkOperations
与 SQL 语句中的参数一样，使用**SQLBulk 操作**或**SQLSetPos**更新行或使用**SQLBulk 操作**插入行时，可以发送长数据。 数据分件发送，对**SQLPutData**进行多次调用。 在执行时发送数据的列称为*执行时的数据列*。  
  
> [!NOTE]  
>  应用程序实际上可以使用**SQLPutData**在执行时发送任何类型的数据，尽管只能分批发送字符和二进制数据。 但是，如果数据足够小，可以容纳单个缓冲区，则通常没有理由使用**SQLPutData**。 绑定缓冲区并让驱动程序从缓冲区检索数据要容易得多。  
  
 由于长数据列通常不绑定，因此应用程序必须在调用**SQLBulk 操作**或**SQLSetPos**之前绑定列，并在调用**SQLBulk 操作**或**SQLSetPos**后取消绑定该列。 必须绑定该列，因为**SQLBulk 操作**或**SQLSetPos**仅在绑定列上操作，并且必须取消绑定，以便**SQLGetData**可用于从列中检索数据。  
  
 要在执行时发送数据，应用程序执行以下操作：  
  
1.  在行集缓冲区中放置 32 位值，而不是数据值。 此值稍后将返回到应用程序，因此应用程序应将其设置为有意义的值，例如列数或包含数据的文件的句柄。  
  
2.  将长度/指示器缓冲区中的值设置为 SQL_LEN_DATA_AT_EXEC（*长度*） 宏的结果。 此值向驱动程序指示参数的数据将与**SQLPutData**一起发送。 将长数据发送到数据源时，将使用*长度*值，数据源需要知道将发送多少字节的长数据，以便它可以预分配空间。 要确定数据源是否需要此值，应用程序使用SQL_NEED_LONG_DATA_LEN选项调用**SQLGetInfo。** 所有驱动程序都必须支持此宏;所有驱动程序都必须支持此宏。如果数据源不需要字节长度，驱动程序可以忽略它。  
  
3.  调用**SQLBulk 操作或** **SQLSetPos**。 驱动程序发现长度/指示器缓冲区包含SQL_LEN_DATA_AT_EXEC（*长度*）宏的结果，并将返回SQL_NEED_DATA作为函数的返回值。  
  
4.  调用**SQLParamData**以响应SQL_NEED_DATA返回值。 如果需要发送长数据 **，SQLParamData**将返回SQL_NEED_DATA。 在*ValuePtrPtr*参数指向的缓冲区中，驱动程序返回应用程序放置在行集缓冲区中的唯一值。 如果存在多个执行数据列，则应用程序使用此值来确定要为其发送数据的列;驱动程序不需要按任何特定顺序请求数据执行列的数据。  
  
5.  调用**SQLPutData**将列数据发送到驱动程序。 如果列数据不适合单个缓冲区（与长数据通常的情况一样），应用程序将重复调用 SQLPutData 以分部发送数据;如果列数据与长数据一样，则调用 SQLPutData 以发送部分数据;如果列数据不适合使用，则调用**SQLPutData**以部分发送数据。由驱动程序和数据源重新组合数据。 如果应用程序传递 null 终止字符串数据，驱动程序或数据源必须删除 null 终止字符作为重新组装过程的一部分。  
  
6.  再次调用**SQLParamData**以指示它已发送了该列的所有数据。 如果有任何未为其发送数据的数据执行列，则驱动程序将返回SQL_NEED_DATA和下一个执行数据列的唯一值;应用程序返回到步骤 5。 如果已为执行时的所有数据列发送数据，则该行的数据将发送到数据源。 **然后，SQLParamData**返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，并可以返回**SQLBulk 操作**或**SQLSetPos**可以返回的任何 SQLSTATE。  
  
 **在 SQLBulk 操作**或**SQLSetPos**返回SQL_NEED_DATA后，在已为执行时的最后一个数据列完全发送数据之前，该语句处于"需要数据"状态。 在此状态下，应用程序只能调用 SQLPutData、SQLParamData、SQLCancel、SQLGetDiagField 或**SQLGetDiagRec;** **SQLPutData** **SQLParamData** **SQLCancel** **SQLGetDiagField**所有其他函数返回 SQLSTATE HY010（函数序列错误）。 调用**SQLCancel**会取消语句的执行并将其返回到其以前的状态。 有关详细信息，请参阅附录[B：ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
