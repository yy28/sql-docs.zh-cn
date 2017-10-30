---
title: "发送的长整型数据 |Microsoft 文档"
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
- long data [ODBC]
- sending long data [ODBC]
ms.assetid: ea989084-a8e6-4737-892e-9ec99dd49caf
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 1f2fad149692bf76c118837daf05e0b77ebf4c38
ms.contentlocale: zh-cn
ms.lasthandoff: 09/09/2017

---
# <a name="sending-long-data"></a>发送的长整型数据
Dbms 定义*长整型数据*作为任何字符或通过某些大小，例如 254 个字符的二进制数据。 它可能不能将整个项的长整型数据存储在内存中，如当该项表示长文本文档或位图。 由于此类数据不能存储在单个缓冲区中，数据源将其发送到使用部件中的驱动程序**SQLPutData**时执行的语句。 在执行时为其发送数据的参数名为*执行中的数据参数*。  
  
> [!NOTE]  
>  应用程序可以在执行时与实际发送任何类型的数据**SQLPutData**，但可以在部件中发送仅字符和二进制数据。 但是，如果数据不足够小，无法放在单个缓冲区，则通常无需使用**SQLPutData**。 它是可以更轻松地将绑定缓冲区，并允许从缓冲区中检索数据的驱动程序。  
  
 若要在执行时发送数据，应用程序，请执行以下操作：  
  
1.  将一个 32 位值，标识中的参数传递*ParameterValuePtr*中的参数**SQLBindParameter**而不是传递缓冲区的地址。 此值不分析驱动程序。 它将返回到更高版本，该应用程序，以便它应表示为应用程序的地方。 例如，它可能是文件的参数的数目或包含数据的句柄。  
  
2.  将传递中的长度/指示器缓冲区的地址*StrLen_or_IndPtr*参数**SQLBindParameter**。  
  
3.  存储 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 的结果 (*长度*) 长度/指示器缓冲区中的宏。 这些值指示的驱动程序参数的数据将与发送到**SQLPutData**。 SQL_LEN_DATA_AT_EXEC (*长度*) 将长整型数据发送到需要知道将发送多少字节的长整型数据，以便它可以预分配空间的数据源时使用。 若要确定在应用程序数据源需要此值，是否调用**SQLGetInfo** SQL_NEED_LONG_DATA_LEN 选项。 所有驱动程序必须支持此宏;如果数据源不需要的字节长度，该驱动程序可以忽略它。  
  
4.  调用**SQLExecute**或**SQLExecDirect**。 该驱动程序发现长度/指示器缓冲区包含值 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC 的结果 (*长度*) 宏并返回 SQL_NEED_DATA 用作函数的返回值。  
  
5.  调用**SQLParamData** SQL_NEED_DATA 响应返回值。 如果长整型数据需要发送， **SQLParamData**返回 SQL_NEED_DATA。 指向的缓冲区中*ValuePtrPtr*自变量，该驱动程序返回标识数据在执行参数的值。 如果有多个数据在执行参数，应用程序必须使用此值来确定哪个参数发送数据;该驱动程序不需要请求按任何特定顺序执行中的数据参数的数据。  
  
6.  调用**SQLPutData**将参数数据发送到该驱动程序。 如果参数数据不适合单个缓冲区，因为通常是长整型数据这种情况，在应用程序调用**SQLPutData**反复将数据发送的部分; 由驱动程序和数据源，来重组数据。 如果应用程序传递 null 结尾的字符串数据，驱动程序或数据源必须删除重组过程的一部分的 null 终止字符。  
  
7.  调用**SQLParamData**再次以指示它是否已发送所有参数的数据。 如果没有为其数据未发送任何数据在执行参数，该驱动程序返回 SQL_NEED_DATA 和标识的下一步的参数; 的值在应用程序返回到步骤 6。 如果已将数据发送所有数据在执行参数，则执行语句。 **SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 和可以返回任何返回值或诊断， **SQLExecute**或**SQLExecDirect**可以返回。  
  
 后**SQLExecute**或**SQLExecDirect**返回 SQL_NEED_DATA，并且数据已完全发送的最后一个的数据在执行参数之前，该语句是否处于需要数据状态。 需要数据状态语句时，应用程序可以调用仅**SQLPutData**， **SQLParamData**， **SQLCancel**， **SQLGetDiagField**，或**SQLGetDiagRec**; 所有其他函数返回 SQLSTATE HY010 （函数序列错误）。 调用**SQLCancel**取消执行语句，并将其返回到以前的状态。 有关详细信息，请参阅[附录 b: ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 在执行时发送数据的示例，请参阅[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)函数说明。

