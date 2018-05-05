---
title: 诊断记录和字段 |Microsoft 文档
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-odbc-error-messages
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- header records [ODBC]
- SQL Server Native Client ODBC driver, errors
- messages [ODBC], diagnostic records
- ODBC error handling, diagnostic records
- SQLGetDiagField function
- diagnostic records [ODBC]
- errors [ODBC], diagnostic records
- fields [ODBC]
- status information [ODBC]
ms.assetid: 4949530c-62d1-4f1a-b592-144244444ce0
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: d9dfbebe695b3c85631ba8e3c44d9a8fe404da37
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="diagnostic-records-and-fields"></a>诊断记录和字段
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  诊断记录与 ODBC 环境、连接、语句或描述符句柄关联。 当任何 ODBC 函数产生的返回代码不是 SQL_SUCCESS 或 SQL_INVALID_HANDLE 时，该函数调用的句柄就有相关联的诊断记录，其中包含信息性或错误性消息。 这些记录会一直保留，直到要通过该句柄调用其他函数，那时，记录就会被丢弃。 与一个句柄任一次调用相关联的诊断记录数目不受限制。  
  
 有两种类型的诊断记录：标题和状态。 标题记录为记录 0；状态记录为记录 1 及更大数字。 诊断记录包含适用于标题记录和状态记录的不同字段。 ODBC 组件还可以定义自己的诊断记录字段。  
  
 标题记录中的字段包含有关函数执行的一般信息，包括返回代码、行计数、状态记录数和所执行的语句的类型。 除非 ODBC 函数返回 SQL_INVALID_HANDLE，否则，总是会创建标题记录。 标头记录中的字段的完整列表，请参阅[SQLGetDiagField](../../relational-databases/native-client-odbc-api/sqlgetdiagfield.md)。  
  
 状态记录中的字段包含关于 ODBC 驱动程序管理器、驱动程序或数据源返回的特定错误或警告的信息，包括 SQLSTATE、本机错误号、诊断消息、列号和行号。 仅当函数返回 SQL_ERROR, SQL_SUCCESS_WITH_INFO、SQL_NO_DATA、SQL_NEED_DATA 或 SQL_STILL_EXECUTING 时，才会创建状态记录。 中的状态记录的字段的完整列表，请参阅**SQLGetDiagField**。  
  
 **SQLGetDiagRec**检索以及其 ODBC SQLSTATE、 本机错误号和诊断消息字段的单个诊断记录。 此功能是类似于 ODBC 2。*x * * * SQLError** 函数。 ODBC 3 中的最简单的错误处理函数。*x*是重复调用**SQLGetDiagRec**开头*RecNumber*参数设置为 1 和递增*RecNumber*直到 1**SQLGetDiagRec**返回 SQL_NO_DATA。 这相当于 ODBC 2。*x*应用程序调用**SQLError**直到它返回 SQL_NO_DATA_FOUND。  
  
 ODBC 3。*x*支持比 ODBC 2 的更多诊断信息。*x*。 此信息存储在中使用检索到的诊断记录的附加字段**SQLGetDiagField**。  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序具有可以使用检索的特定于驱动程序的诊断字段**SQLGetDiagField**。 这些特定于驱动程序的字段的标签在 sqlncli.h 中定义。 使用这些标签可以检索与每条诊断记录关联的 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 状态、严重级别、服务器名称、过程名称和行号。 此外，sqlncli.h 包含的驱动程序使用标识 TRANSACT-SQL 语句，如果应用程序调用的代码定义**SQLGetDiagField**与*DiagIdentifier*设置为 SQL_DIAG_DYNAMIC_FUNCTION_CODE。  
  
 **SQLGetDiagField**是 ODBC 驱动程序管理器处理的使用它从基础驱动程序缓存的错误信息。 在成功连接之前，ODBC 驱动程序管理器不会缓存特定于驱动程序的诊断字段。 **SQLGetDiagField**返回 SQL_ERROR，如果它调用以完成成功的连接之前获取特定于驱动程序的诊断字段。 如果 ODBC 连接函数返回 SQL_SUCCESS_WITH_INFO，则该连接函数特定于驱动程序的诊断字段尚不可用。 你可以调用**SQLGetDiagField**特定于驱动程序的诊断字段仅后所做的另一个 ODBC 连接函数之后函数调用。  
  
 报告的大多数错误[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序可以有效地使用诊断仅返回的信息**SQLGetDiagRec**。 不过，在有些情况下，特定于驱动程序的诊断字段返回的信息对于诊断错误非常重要。 编码的 ODBC 错误处理程序使用的应用程序时[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序，它是一个好办法还使用**SQLGetDiagField**检索至少 SQL_DIAG_SS_MSGSTATE 和 SQL_DIAG_SS_SEVERITY特定于驱动程序的字段。 如果特定错误可以在 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 代码的多个位置引发，SQL_DIAG_SS_MSGSTATE 会为 Microsoft 支持工程师专门指示错误的引发位置，有时，这有助于诊断问题。  
  
## <a name="see-also"></a>另请参阅  
 [处理错误和消息](../../relational-databases/native-client-odbc-error-messages/handling-errors-and-messages.md)  
  
  
