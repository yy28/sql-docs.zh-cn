---
title: Long 数据和 SQLSetPos 及 SQLBulkOperations |Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b1d1a55d3b417ff7a0a673bda8d289a72d7c1cb1
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/01/2018
ms.locfileid: "47658425"
---
# <a name="long-data-and-sqlsetpos-and-sqlbulkoperations"></a>Long 数据和 SQLSetPos 及 SQLBulkOperations
更新行时在 SQL 语句中使用参数的情况一样，可以发送长数据**SQLBulkOperations**或**SQLSetPos**或插入的行时**SQLBulkOperations**. 将数据发送中使用多个调用部件**SQLPutData**。 在执行时为其发送数据的列被称为*执行时数据列*。  
  
> [!NOTE]  
>  应用程序实际上可以将发送任何类型的数据在执行时使用**SQLPutData**，尽管可以在部件中发送仅字符和二进制数据。 但是，如果数据是足够小，无法全部放入一个缓冲区，则通常无需使用**SQLPutData**。 它是更轻松地将缓冲区绑定和让驱动程序从缓冲区检索数据。  
  
 因为通常未绑定的长整型数据列，应用程序必须将绑定的列之前调用**SQLBulkOperations**或**SQLSetPos**和之后调用 unbind **SQLBulkOperations**或**SQLSetPos**。 必须绑定列，因为**SQLBulkOperations**或**SQLSetPos**只对绑定列执行操作，并且必须未绑定，以便**SQLGetData**可用于检索数据从列中。  
  
 若要在执行时发送数据，应用程序执行以下任务：  
  
1.  在行集而不是数据值的缓冲区中放入一个 32 位值。 将向应用程序更高版本，返回此值，因此应用程序应将其设置为有意义的值，如列数或包含数据的文件的句柄。  
  
2.  设置为 SQL_LEN_DATA_AT_EXEC 结果的长度/指示器缓冲区中的值 (*长度*) 宏。 此值指示驱动程序的参数的数据将发送具有**SQLPutData**。 *长度*将长整型数据发送到的数据源，需要知道将发送长数据的字节数，以便它可以预分配空间时使用值。 若要确定数据源是否需要此值，应用程序调用**SQLGetInfo** SQL_NEED_LONG_DATA_LEN 选项。 所有驱动程序必须支持此宏;如果数据源不需要的字节长度，则驱动程序可以忽略它。  
  
3.  调用**SQLBulkOperations**或**SQLSetPos**。 该驱动程序发现长度/指示器缓冲区包含结果的 SQL_LEN_DATA_AT_EXEC (*长度*) 宏，并返回该函数的返回值为 SQL_NEED_DATA。  
  
4.  调用**SQLParamData** SQL_NEED_DATA 响应中返回的值。 如果需要发送长数据**SQLParamData**返回 SQL_NEED_DATA。 在通过指向的缓冲区*ValuePtrPtr*参数，驱动程序返回应用程序放置在行集的缓冲区中的唯一值。 如果有多个执行时数据列，应用程序使用此值以确定哪一列发送数据;该驱动程序不需要请求按任何特定顺序执行时数据列的数据。  
  
5.  调用**SQLPutData**将列数据发送到该驱动程序。 如果列数据不适合在单个缓冲区中，通常会与长数据的情况是，应用程序调用**SQLPutData**反复将数据发送部分; 由驱动程序和数据源来重组数据。 如果应用程序将以 null 结尾的字符串数据传递，驱动程序或数据源必须删除作为重组过程的一部分的 null 终止字符。  
  
6.  调用**SQLParamData**再次以指示它已发送的所有列的数据。 如果尚未发送的数据的任何执行时数据列，驱动程序将返回 SQL_NEED_DATA 和下一步执行时数据列中; 的唯一值应用程序返回到步骤 5。 如果数据已发送的所有执行时数据列，行的数据是发送到数据源。 **SQLParamData** ，然后再返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 和可以返回任何 SQLSTATE **SQLBulkOperations**或**SQLSetPos**可以返回。  
  
 之后**SQLBulkOperations**或**SQLSetPos**返回 SQL_NEED_DATA 和最后一个执行时数据列已完全将数据之前，该语句是处于需要的数据状态。 在此状态下，应用程序可以调用仅**SQLPutData**， **SQLParamData**， **SQLCancel**， **SQLGetDiagField**，或**SQLGetDiagRec**; 所有其他函数都返回 SQLSTATE HY010 （函数序列错误）。 调用**SQLCancel**取消该语句的执行并将其返回到其以前的状态。 有关详细信息，请参阅[附录 b: ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。
