---
title: SQLBindCol |微软文档
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 69457daccbc7868e58f91c71a48b4b25f15f5318
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302700"
---
# <a name="sqlbindcol"></a>SQLBindCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  通常，请考虑使用**SQLBindCol**导致数据转换的含义。 绑定转换是客户端进程，所以，举例来说，检索绑定到字符列的浮点值将导致应用程序在提取行时执行浮点到字符的转换。 可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CONVERT 函数将数据转换的开销转给服务器。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例可以对执行的单个语句返回多个结果行集。 每个结果集都必须单独绑定。 有关多个结果集的绑定的详细信息，请参阅[SQLMore 结果](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。  
  
 开发人员可以使用[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]*目标类型*值**SQL_C_BINARY**将列绑定到特定的 C 数据类型。 不可移植绑定到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定类型的列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定的已定义 ODBC C 数据类型与 DB-Library 的类型定义匹配，移植应用程序的 DB-Library 开发人员可能需要利用此功能。  
  
 对于[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序，报告数据截断是一个昂贵的过程。 通过确保所有绑定数据缓冲区的宽度足以返回数据，可以避免截断。 对于字符数据，在使用字符串终止的默认驱动程序行为时，该宽度应该包括字符串终止符所占的空间。 例如，将[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char（5）** 列绑定到包含五个字符的数组，会导致获取的每个值都截断。 将同一列绑定到六个字符的数组可以提供一个用于存储空终止符的字符元素，这样即避免了截断。 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)可用于高效地检索长字符和二进制数据，而不会截断。  
  
 对于较大的值数据类型，如果用户提供的缓冲区不够大，无法容纳列的整个值，则返回**SQL_SUCCESS_WITH_INFO**并返回"字符串数据;如果用户提供的缓冲区不足以容纳列的整个值。"发出右截断"警告。 **StrLen_or_IndPtr**参数将包含存储在缓冲区中的字符/字节数。  
  
## <a name="sqlbindcol-support-for-enhanced-date-and-time-features"></a>SQLBindCol 对日期和时间增强功能的支持  
 日期/时间类型的结果列值将转换，如从[SQL 到 C 的转换](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)中所述。请注意，要检索时间和日期时间偏移列作为其相应的结构 **（SQL_SS_TIME2_STRUCT**和**SQL_SS_TIMESTAMPOFFSET_STRUCT），***必须指定为***SQL_C_DEFAULT**或**SQL_C_BINARY。**  
  
 有关详细信息，请参阅[&#40;ODBC&#41;的日期和时间改进](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlbindcol-support-for-large-clr-udts"></a>SQLBindCol 对大型 CLR UDT 的支持  
 **SQLBindCol**支持大型 CLR 用户定义类型 （UDT）。 有关详细信息，请参阅[&#40;ODBC&#41;的大型 CLR 用户定义类型](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLBindCol 函数](https://go.microsoft.com/fwlink/?LinkId=59327)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
