---
description: 发送 Long 数据
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f6a0ec1a7e8dc703d3e7a3ed5332d20e6539eafe
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476459"
---
# <a name="sending-long-data"></a>发送 Long 数据
Dbms 将 *长数据* 定义为一定大小的任何字符或二进制数据，例如254个字符。 可能无法将长数据的整个项存储在内存中，如项表示长文本文档或位图。 由于此类数据无法存储在单个缓冲区中，因此在执行语句时，数据源会将其发送到包含 **SQLPutData** 的部分中的驱动程序。 用于在执行时发送数据的参数称为 "执行时 *数据" 参数*。  
  
> [!NOTE]  
>  应用程序可以在执行时实际通过 **SQLPutData**发送任意类型的数据，尽管只能在部分中发送字符和二进制数据。 但是，如果数据太小，足以容纳在单个缓冲区中，通常没有理由使用 **SQLPutData**。 绑定缓冲区并让驱动程序从缓冲区中检索数据，这要简单得多。  
  
 若要在执行时发送数据，应用程序需要执行以下操作：  
  
1.  在**SQLBindParameter**中传递标识*ParameterValuePtr*参数中的参数的32位值，而不是传递缓冲区的地址。 驱动程序不会分析此值。 稍后会将其返回给应用程序，因此应用程序的意思应该是什么。 例如，它可能是参数的编号或包含数据的文件的句柄。  
  
2.  在**SQLBindParameter**的*StrLen_or_IndPtr*参数中传递长度/指示器缓冲区的地址。  
  
3.  将 SQL_DATA_AT_EXEC 或 SQL_LEN_DATA_AT_EXEC (*长度*) 宏的结果存储在长度/指示器缓冲区中。 这两个值向驱动程序指示参数的数据将与 **SQLPutData**一起发送。 向数据源发送长数据时，将使用 SQL_LEN_DATA_AT_EXEC (*长度*) ，该数据源需要知道将发送多少字节的长数据以便它能够预分配空间。 若要确定数据源是否需要此值，应用程序需要使用 SQL_NEED_LONG_DATA_LEN 选项调用 **SQLGetInfo** 。 所有驱动程序都必须支持此宏;如果数据源不需要字节长度，则驱动程序可以忽略此长度。  
  
4.  调用 **SQLExecute** 或 **SQLExecDirect**。 驱动程序发现长度/指示器缓冲区包含 SQL_LEN_DATA_AT_EXEC (*长度*) 宏的值 SQL_DATA_AT_EXEC 或结果，并将 SQL_NEED_DATA 作为函数的返回值返回。  
  
5.  调用 **SQLParamData** 以响应 SQL_NEED_DATA 返回值。 如果需要发送长数据， **SQLParamData** 返回 SQL_NEED_DATA。 在由 *ValuePtrPtr* 参数指向的缓冲区中，驱动程序将返回标识执行时数据参数的值。 如果有多个执行时数据参数，则应用程序必须使用此值来确定要为其发送数据的参数;该驱动程序不要求以任何特定顺序为执行时数据参数请求数据。  
  
6.  调用 **SQLPutData** 将参数数据发送给驱动程序。 如果参数数据不适用于单个缓冲区，通常情况下，长数据的情况下，应用程序会重复调用 **SQLPutData** 以在部分中发送数据;驱动程序和数据源由驱动程序和数据源组成，用于重组数据。 如果应用程序传递了以 null 结尾的字符串数据，则驱动程序或数据源必须删除 null 终止字符作为重汇编过程的一部分。  
  
7.  再次调用 **SQLParamData** ，以指示它已发送参数的所有数据。 如果有数据尚未发送的任何执行时数据参数，则驱动程序将返回 SQL_NEED_DATA 和标识下一个参数的值;应用程序返回到步骤6。 如果为所有执行时数据参数发送了数据，则执行该语句。 **SQLParamData** 返回 SQL_SUCCESS 或 SQL_SUCCESS_WITH_INFO，可以返回 **SQLExecute** 或 **SQLExecDirect** 可以返回的任何返回值或诊断。  
  
 在 **SQLExecute** 或 **SQLExecDirect** 返回 SQL_NEED_DATA 之后，在为最后一个执行时数据参数完全发送数据之前，该语句处于需要数据状态。 当语句处于需要数据状态时，应用程序只能调用 **SQLPutData**、 **SQLParamData**、 **SQLCancel**、 **SQLGetDiagField**或 **SQLGetDiagRec**;所有其他函数都返回 SQLSTATE HY010 (函数序列错误) 。 调用 **SQLCancel** 将取消语句的执行，并将其返回到它以前的状态。 有关详细信息，请参阅 [附录 B： ODBC 状态转换表](../../../odbc/reference/appendixes/appendix-b-odbc-state-transition-tables.md)。  
  
 有关在执行时发送数据的示例，请参阅 [SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md) 函数说明。
