---
title: SQLBindCol |Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
topic_type:
- apiref
helpviewer_keywords:
- SQLBindCol function
ms.assetid: fbd7ba20-d917-4ca9-b018-018ac6af9f98
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: d8f4a04d7851a79ab461711cfc173d40a0a83ef6
ms.sourcegitcommit: b72c9fc9436c44c6a21fd96223c73bf94706c06b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/01/2020
ms.locfileid: "82706401"
---
# <a name="sqlbindcol"></a>SQLBindCol
  作为一般规则，请考虑使用**SQLBindCol**导致数据转换的含义。 绑定转换是客户端进程，所以，举例来说，检索绑定到字符列的浮点值将导致应用程序在提取行时执行浮点到字符的转换。 可以使用 [!INCLUDE[tsql](../../includes/tsql-md.md)] CONVERT 函数将数据转换的开销转给服务器。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 实例可以对执行的单个语句返回多个结果行集。 每个结果集都必须单独绑定。 有关多个结果集的绑定的详细信息，请参阅[SQLMoreResults](sqlmoreresults.md)。  
  
 开发人员可以使用 TargetType 值将列绑定到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定的 C *TargetType*数据类型 `SQL_C_BINARY` 。 不可移植绑定到 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定类型的列。 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 特定的已定义 ODBC C 数据类型与 DB-Library 的类型定义匹配，移植应用程序的 DB-Library 开发人员可能需要利用此功能。  
  
 对于 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native CLIENT ODBC 驱动程序，报告数据截断是一种开销高昂的过程。 通过确保所有绑定数据缓冲区的宽度足以返回数据，可以避免截断。 对于字符数据，在使用字符串终止的默认驱动程序行为时，该宽度应该包括字符串终止符所占的空间。 例如，如果将 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **char （5）** 列绑定到五个字符，则会导致每个提取的值被截断。 将同一列绑定到六个字符的数组可以提供一个用于存储空终止符的字符元素，这样即避免了截断。 [SQLGetData](sqlgetdata.md)可用于在不截断的情况下有效地检索长字符和二进制数据。  
  
 对于大值数据类型，如果用户提供的缓冲区不够大，无法保存列的整个值， `SQL_SUCCESS_WITH_INFO` 则返回，并返回 "字符串数据;发出右截断 "警告。 `StrLen_or_IndPtr` 参数将包含存储在缓冲区中的字符/字节数。  
  
## <a name="sqlbindcol-support-for-enhanced-date-and-time-features"></a>SQLBindCol 对日期和时间增强功能的支持  
 日期/时间类型的结果列值按[从 SQL 到 C 的转换](../native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)中所述进行转换。请注意，若要检索时间和 datetimeoffset 列作为其相应的结构（ `SQL_SS_TIME2_STRUCT` 和**SQL_SS_TIMESTAMPOFFSET_STRUCT**），必须将*TargetType*指定为 `SQL_C_DEFAULT` 或 `SQL_C_BINARY` 。  
  
 有关详细信息，请参阅[ODBC&#41;&#40;日期和时间改进](../native-client-odbc-date-time/date-and-time-improvements-odbc.md)。  
  
## <a name="sqlbindcol-support-for-large-clr-udts"></a>SQLBindCol 对大型 CLR UDT 的支持  
 **SQLBindCol**支持大型 CLR 用户定义类型（udt）。 有关详细信息，请参阅[&#40;ODBC&#41;的大型 CLR 用户定义类型](../native-client/odbc/large-clr-user-defined-types-odbc.md)。  
  
## <a name="see-also"></a>另请参阅  
 [SQLBindCol 函数](https://go.microsoft.com/fwlink/?LinkId=59327)   
 [ODBC API 实现细节](odbc-api-implementation-details.md)  
  
  
