---
title: 发送长数据 |Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- long data [ODBC]
- sending long data [ODBC]
ms.assetid: ea989084-a8e6-4737-892e-9ec99dd49caf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cc7a140d7de8548f02fde6ab309823bbe1c9c656
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2019
ms.locfileid: "62465917"
---
# <a name="sending-long-data"></a>发送 Long 数据
定义 Dbms*长整型数据*为任何字符或二进制数据而非特定大小，如 254 个字符。 可能无法用于存储在内存中，如时项所表示的长文本文档或位图的长数据的整个项目。 由于此类数据不能存储在一个缓冲区，数据源将其发送到使用部件中的驱动程序**SQLPutData**时执行的语句。 在执行时为其发送数据的参数称为*执行时数据参数*。  
  
> [!NOTE]  
>  应用程序可以将任何类型的数据实际发送在执行时使用**SQLPutData**，尽管可以在部件中发送仅字符和二进制数据。 但是，如果数据是足够小，无法全部放入一个缓冲区，则通常无需使用**SQLPutData**。 它是更轻松地将缓冲区绑定和让驱动程序从缓冲区检索数据。  
  
 若要在执行时发送数据，应用程序，请执行以下操作：  
  
1.  将 32 位值，用于标识中的参数传递*ParameterValuePtr*中的参数**SQLBindParameter**而不是传递的缓冲区的地址。 此值不会分析驱动程序。 它将返回到更高版本，该应用程序，因此它应表示为应用程序的地方。 例如，它可能是文件的参数的编号或包含数据的句柄。  
  
2.  将传递中的长度/指示器缓冲区的地址*StrLen_or_IndPtr*的参数**SQLBindParameter**。  
  
3.  存储 SQL_DATA_AT_EXEC 或结果 SQL_LEN_DATA_AT_EXEC (*长度*) 长度/指示器缓冲区中的宏。 这两种值指示驱动程序的参数的数据将发送具有**SQLPutData**。 SQL_LEN_DATA_AT_EXEC (*长度*) 长数据发送到的数据源，需要知道将发送长数据的字节数，以便它可以预分配空间时使用。 若要确定应用程序的数据源，需要此值，是否调用**SQLGetInfo** SQL_NEED_LONG_DATA_LEN 选项。 所有驱动程序必须支持此宏;如果数据源不需要的字节长度，则驱动程序可以忽略它。  
  
4.  调用**SQLExecute**或**SQLExecDirect**。 该驱动程序发现长度/指示器缓冲区包含值 SQL_DATA_AT_EXEC 或结果 SQL_LEN_DATA_AT_EXEC (*长度*) 宏，并返回该函数的返回值为 SQL_NEED_DATA。  
  
5.  调用**SQLParamData** SQL_NEED_DATA 响应中返回的值。 如果需要发送长数据**SQLParamData**返回 SQL_NEED_DATA。 在通过指向的缓冲区*ValuePtrPtr*参数，驱动程序将返回标识执行时数据参数的值。 如果多个执行时数据参数，该应用程序必须使用此值来确定哪些参数来发送数据;该驱动程序不需要请求中任何特定顺序执行时数据参数的数据。  
  
6.  调用**SQLPutData**将参数数据发送到该驱动程序。 如果参数数据不适合单个缓冲区中，通常会与长数据的情况是，应用程序调用**SQLPutData**反复将数据发送部分; 由驱动程序和数据源来重组数据。 如果应用程序将以 null 结尾的字符串数据传递，驱动程序或数据源必须删除作为重组过程的一部分的 null 终止字符。  
  
7.  调用**SQLParamData**再次以指示它已发送所有参数的数据。 如果尚未发送的数据的任何执行时数据参数，驱动程序将返回 SQL_NEED_DATA 和标识的下一个参数; 的值应用程序返回到步骤 6。 如果数据已发送的所有执行时数据参数，则执行该语句。 **SQLParamData**返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO 和可以返回任何返回值或诊断， **SQLExecute**或**SQLExecDirect**可以返回。  
  
 之后**SQLExecute**或**SQLExecDirect**返回 SQL_NEED_DATA 和最后一个执行时数据参数已完全将数据之前，该语句是处于需要的数据状态。 需要数据状态语句时，应用程序可以调用仅**SQLPutData**， **SQLParamData**， **SQLCancel**， **SQLGetDiagField**，或**SQLGetDiagRec**; 所有其他函数都返回 SQLSTATE HY010 （函数序列错误）。 调用**SQLCancel**取消该语句的执行并将其返回到其以前的状态。 有关详细信息，请参阅[附录 b:状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 在执行时发送数据的示例，请参阅[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)函数说明。
