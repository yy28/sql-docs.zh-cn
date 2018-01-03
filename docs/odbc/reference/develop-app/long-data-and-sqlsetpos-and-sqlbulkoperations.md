---
title: "Long 数据和 SQLSetPos 和 SQLBulkOperations |Microsoft 文档"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- long data [ODBC]
- SQLSetPos function [ODBC], long data and SQLBulkOperations
- data updates [ODBC], long data
- updating data [ODBC], long data
- SQLBulkOperations function [ODBC], long data
ms.assetid: e2fdf842-5e4c-46ca-bb21-4625c3324f28
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 7684c15df244828211c2b87acd7314a7e05bea5e
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/21/2017
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Long 数据和 SQLSetPos 和 SQLBulkOperations
当更新行与在 SQL 语句中使用参数情况一样，可以发送的长整型数据**SQLBulkOperations**或**SQLSetPos**或插入的行时**SQLBulkOperations**. 将数据发送在部件中，通过多个调用**SQLPutData**。 在执行时为其发送数据的列称为*执行中的数据列*。  
  
> [!NOTE]  
>  应用程序实际上可以发送任何类型的数据在执行时使用**SQLPutData**，但可以在部件中发送仅字符和二进制数据。 但是，如果数据不足够小，无法放在单个缓冲区，则通常无需使用**SQLPutData**。 它是可以更轻松地将绑定缓冲区，并允许从缓冲区中检索数据的驱动程序。  
  
 因为通常未绑定的长整型数据列，应用程序必须将绑定之前调用列**SQLBulkOperations**或**SQLSetPos**和取消它绑定之后调用**SQLBulkOperations**或**SQLSetPos**。 必须将绑定列，因为**SQLBulkOperations**或**SQLSetPos**仅仅作用于绑定的列，并且必须未绑定，以便**SQLGetData**可以用于检索数据从列。  
  
 若要在执行时发送数据，应用程序执行以下任务：  
  
1.  将一个 32 位值放在而不是数据值的行集缓冲区。 此值将返回到更高版本，该应用程序中，以便应用程序应将其设置为有意义的值，如列数或包含数据的文件的句柄。  
  
2.  设置 SQL_LEN_DATA_AT_EXEC 的结果的长度/指示器缓冲区中的值 (*长度*) 宏。 此值指示的驱动程序参数的数据将发送与**SQLPutData**。 *长度*将长整型数据发送到需要知道将发送多少字节的长整型数据，以便它可以预分配空间的数据源时使用值。 若要确定数据源是否需要此值，则应用程序调用**SQLGetInfo** SQL_NEED_LONG_DATA_LEN 选项。 所有驱动程序必须支持此宏;如果数据源不需要的字节长度，该驱动程序可以忽略它。  
  
3.  调用**SQLBulkOperations**或**SQLSetPos**。 该驱动程序发现长度/指示器缓冲区包含结果的 SQL_LEN_DATA_AT_EXEC (*长度*) 宏并返回 SQL_NEED_DATA 用作函数的返回值。  
  
4.  调用**SQLParamData** SQL_NEED_DATA 响应返回值。 如果长整型数据需要发送， **SQLParamData**返回 SQL_NEED_DATA。 指向的缓冲区中*ValuePtrPtr*自变量，该驱动程序返回应用程序放置在行集的缓冲区中的唯一值。 如果有多个执行中的数据列，应用程序使用此值来确定哪一列中发送数据;该驱动程序不需要请求中的任何特定顺序执行中的数据列的数据。  
  
5.  调用**SQLPutData**将列数据发送到该驱动程序。 如果列数据不适合在单个缓冲区中，因为通常是长整型数据这种情况，在应用程序调用**SQLPutData**反复将数据发送的部分; 由驱动程序和数据源，来重组数据。 如果应用程序传递 null 结尾的字符串数据，驱动程序或数据源必须删除重组过程的一部分的 null 终止字符。  
  
6.  调用**SQLParamData**再次以指示它是否已发送所有列的数据。 如果没有为其数据未发送任何执行中的数据列，该驱动程序返回 SQL_NEED_DATA 和下一步的执行中的数据列; 的唯一值在应用程序返回到步骤 5。 如果已将数据发送所有数据在执行列中，行的数据都发送到数据源。 **SQLParamData** ，然后再返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 和可以返回的任何 SQLSTATE **SQLBulkOperations**或**SQLSetPos**可以返回。  
  
 后**SQLBulkOperations**或**SQLSetPos**返回 SQL_NEED_DATA，并且数据已完全发送的最后一个的执行中的数据列之前，该语句是否处于需要数据状态。 在此状态下，应用程序可以调用仅**SQLPutData**， **SQLParamData**， **SQLCancel**， **SQLGetDiagField**，或**SQLGetDiagRec**; 所有其他函数返回 SQLSTATE HY010 （函数序列错误）。 调用**SQLCancel**取消执行语句，并将其返回到以前的状态。 有关详细信息，请参阅[附录 b: ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
