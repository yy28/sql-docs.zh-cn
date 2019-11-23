---
title: SQLBindCol | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindCol function
ms.assetid: fbd7ba20-d917-4ca9-b018-018ac6af9f98
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 4a92c95a67b6e9fd3d31917af4f5b7b19f4c613d
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73787789"
---
# <a name="sqlbindcol"></a>SQLBindCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  作为一般规则，请考虑使用**SQLBindCol**导致数据转换的含义。 绑定转换是客户端进程，所以，举例来说，检索绑定到字符列的浮点值将导致应用程序在提取行时执行浮点到字符的转换。 可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CONVERT 函数将数据转换的开销转给服务器。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例可以对执行的单个语句返回多个结果行集。 每个结果集都必须单独绑定。 有关多个结果集的绑定的详细信息，请参阅[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。  
  
 开发人员可以使用*TargetType*值**SQL_C_BINARY**将列绑定到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]特定的 C 数据类型。 不可移植绑定到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定类型的列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定的已定义 ODBC C 数据类型与 DB-Library 的类型定义匹配，移植应用程序的 DB-Library 开发人员可能需要利用此功能。  
  
 报表数据截断是 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序的成本高昂的过程。 通过确保所有绑定数据缓冲区的宽度足以返回数据，可以避免截断。 对于字符数据，在使用字符串终止的默认驱动程序行为时，该宽度应该包括字符串终止符所占的空间。 例如，将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char （5）** 列绑定到五个字符的数组将导致每个提取的值都被截断。 将同一列绑定到六个字符的数组可以提供一个用于存储空终止符的字符元素，这样即避免了截断。 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)可用于在不截断的情况下有效地检索长字符和二进制数据。  
  
 对于大值数据类型，如果用户提供的缓冲区不够大，无法保存列的整个值，则会返回**SQL_SUCCESS_WITH_INFO**和 "string data;发出右截断 "警告。 **StrLen_or_IndPtr**参数将包含缓冲区中存储的字符数/字节数。  
  
## <a name="sqlbindcol-support-for-enhanced-date-and-time-features"></a>SQLBindCol 对日期和时间增强功能的支持  
 日期/时间类型的结果列值按[从 SQL 到 C 的转换](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)中所述进行转换。请注意，若要将 time 和 datetimeoffset 列检索为其相应的结构（**SQL_SS_TIME2_STRUCT**和**SQL_SS_TIMESTAMPOFFSET_STRUCT**），则必须将*TargetType*指定为**SQL_C_DEFAULT**或**SQL_C_BINARY**。  
  
 有关详细信息，请参阅[日期和时间&#40;改进&#41;ODBC](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlbindcol-support-for-large-clr-udts"></a>SQLBindCol 对大型 CLR UDT 的支持  
 **SQLBindCol**支持大型 CLR 用户定义类型（udt）。 有关详细信息，请参阅[大型 CLR 用户定义类型&#40;ODBC&#41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLBindCol 函数](https://go.microsoft.com/fwlink/?LinkId=59327)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
