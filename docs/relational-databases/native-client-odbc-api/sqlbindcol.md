---
title: SQLBindCol |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-api
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLBindCol function
ms.assetid: fbd7ba20-d917-4ca9-b018-018ac6af9f98
caps.latest.revision: 39
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3dce23669637b9fd39e9fa84d37600bae6e64f98
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlbindcol"></a>SQLBindCol
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  作为一般规则，请考虑使用的影响的**SQLBindCol**若要使数据转换。 绑定转换是客户端进程，所以，举例来说，检索绑定到字符列的浮点值将导致应用程序在提取行时执行浮点到字符的转换。 可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CONVERT 函数将数据转换的开销转给服务器。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例可以对执行的单个语句返回多个结果行集。 每个结果集都必须单独绑定。 有关多个结果集的绑定的详细信息，请参阅[SQLMoreResults](../../relational-databases/native-client-odbc-api/sqlmoreresults.md)。  
  
 开发人员可以将列绑定到[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-使用特定 C 数据类型*TargetType*值**SQL_C_BINARY**。 不可移植绑定到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定类型的列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定的已定义 ODBC C 数据类型与 DB-Library 的类型定义匹配，移植应用程序的 DB-Library 开发人员可能需要利用此功能。  
  
 报告数据截断是代价高昂的过程为[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序。 通过确保所有绑定数据缓冲区的宽度足以返回数据，可以避免截断。 对于字符数据，在使用字符串终止的默认驱动程序行为时，该宽度应该包括字符串终止符所占的空间。 例如，绑定[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char(5)** 到数组中提取每个值的截断的五个字符结果的列。 将同一列绑定到六个字符的数组可以提供一个用于存储空终止符的字符元素，这样即避免了截断。 [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md)可用来高效地检索长字符和二进制数据而不发生截断。  
  
 对于大型值数据类型，如果用户提供缓冲区不够大到能够容纳的列，整个值**SQL_SUCCESS_WITH_INFO**返回和"字符串数据;发出右截断"警告。 **StrLen_or_IndPtr**自变量将包含的字符/存储在缓冲区中的字节数。  
  
## <a name="sqlbindcol-support-for-enhanced-date-and-time-features"></a>SQLBindCol 对日期和时间增强功能的支持  
 结果列的日期/时间类型的值将转换中所述[从 SQL 转换到 C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)。请注意，若要检索作为其相应的结构的时间和 datetimeoffset 列 (**SQL_SS_TIME2_STRUCT**和**SQL_SS_TIMESTAMPOFFSET_STRUCT**)， *TargetType*必须指定为**SQL_C_DEFAULT**或**SQL_C_BINARY**。  
  
 有关详细信息，请参阅[日期和时间改进 & #40; ODBC & #41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlbindcol-support-for-large-clr-udts"></a>SQLBindCol 对大型 CLR UDT 的支持  
 **SQLBindCol**支持大型 CLR 用户定义类型 (Udt)。 有关详细信息，请参阅[Large CLR User-Defined 类型 & #40; ODBC & #41;](../../relational-databases/native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLBindCol 函数](http://go.microsoft.com/fwlink/?LinkId=59327)   
 [ODBC API 实现详细信息](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
