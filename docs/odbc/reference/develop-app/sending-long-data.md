---
title: 发送长数据 |微软文档
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: aeeeb716aa2f9a72338f3aeb586dffce86f84069
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304178"
---
# <a name="sending-long-data"></a>发送 Long 数据
DBMS 将*长数据*定义为特定大小的任意字符或二进制数据，例如 254 个字符。 可能无法将整个长数据项存储在内存中，例如当项目表示长文本文档或位图时。 由于此类数据不能存储在单个缓冲区中，因此在执行语句时，数据源会将其发送到**SQLPutData**的部件中的驱动程序。 在执行时发送数据的参数称为*执行时的数据参数*。  
  
> [!NOTE]  
>  应用程序实际上可以使用**SQLPutData**在执行时发送任何类型的数据，尽管只能分批发送字符和二进制数据。 但是，如果数据足够小，可以容纳单个缓冲区，则通常没有理由使用**SQLPutData**。 绑定缓冲区并让驱动程序从缓冲区检索数据要容易得多。  
  
 要在执行时发送数据，应用程序执行以下操作：  
  
1.  传递一个 32 位值，该值标识**SQLBind 参数**中的*参数ValuePtr*参数中的参数，而不是传递缓冲区的地址。 驱动程序不分析此值。 稍后将返回到应用程序，因此对应用程序来说应有一些意义。 例如，它可能是参数的数量或包含数据的文件的句柄。  
  
2.  在**SQLBind 参数***的StrLen_or_IndPtr*参数中传递长度/指示器缓冲区的地址。  
  
3.  将SQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC（*长度*）宏的结果存储在长度/指示器缓冲区中。 这两个值都向驱动程序指示参数的数据将与**SQLPutData**一起发送。 SQL_LEN_DATA_AT_EXEC（*长度*）用于将长数据发送到数据源时，数据源需要知道将发送多少字节的长数据，以便它可以预分配空间。 要确定数据源是否需要此值，应用程序使用SQL_NEED_LONG_DATA_LEN选项调用**SQLGetInfo。** 所有驱动程序都必须支持此宏;所有驱动程序都必须支持此宏。如果数据源不需要字节长度，驱动程序可以忽略它。  
  
4.  调用**SQLExecute**或**SQLExecDirect**。 驱动程序发现长度/指示器缓冲区包含值SQL_DATA_AT_EXEC或SQL_LEN_DATA_AT_EXEC（*长度*）宏的结果，并返回SQL_NEED_DATA作为函数的返回值。  
  
5.  调用**SQLParamData**以响应SQL_NEED_DATA返回值。 如果需要发送长数据 **，SQLParamData**将返回SQL_NEED_DATA。 在*ValuePtrPtr*参数指向的缓冲区中，驱动程序返回标识执行时数据参数的值。 如果有多个执行时的数据参数，则应用程序必须使用此值来确定要为其发送数据的参数;驱动程序不需要按任何特定顺序请求数据执行时参数的数据。  
  
6.  调用**SQLPutData**将参数数据发送到驱动程序。 如果参数数据不适合单个缓冲区（与长数据通常的情况一样），应用程序将重复调用 SQLPutData 以零件发送数据;如果参数数据不适合单个缓冲区，则应用程序将重复调用 SQLPutData 以发送部分数据;如果参数数据不适合，则调用**SQLPutData**以部分发送数据。由驱动程序和数据源重新组合数据。 如果应用程序传递 null 终止字符串数据，驱动程序或数据源必须删除 null 终止字符作为重新组装过程的一部分。  
  
7.  再次调用**SQLParamData**以指示它已发送了参数的所有数据。 如果有任何未发送数据执行时的数据参数，驱动程序将返回SQL_NEED_DATA和标识下一个参数的值;应用程序返回到步骤 6。 如果已为执行时的所有数据参数发送数据，则执行语句。 **SQLParamData**返回SQL_SUCCESS或SQL_SUCCESS_WITH_INFO，并可以返回 SQLExecute 或**SQLExecDirect**可以返回的任何返回值或诊断。 **SQLExecDirect**  
  
 **在 SQLExecute**或**SQLExecDirect**返回SQL_NEED_DATA后，在为上次执行时的数据完全发送数据之前，该语句处于"需要数据"状态。 当语句处于"需要数据"状态时，应用程序只能调用 SQLPutData、SQLParamData、SQLCancel、SQLGetDiagField 或**SQLGetDiagRec;** **SQLPutData** **SQLParamData** **SQLCancel** **SQLGetDiagField**所有其他函数返回 SQLSTATE HY010（函数序列错误）。 调用**SQLCancel**会取消语句的执行并将其返回到其以前的状态。 有关详细信息，请参阅附录[B：ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 有关在执行时发送数据的示例，请参阅[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)函数说明。
