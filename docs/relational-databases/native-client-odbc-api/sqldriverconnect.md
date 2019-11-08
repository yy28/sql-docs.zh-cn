---
title: SQLDriverConnect |Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLDriverConnect function
ms.assetid: a1e38e2c-3a97-42d1-9c45-a0ca3282ffd1
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 9a76a653277b7f99ecf88c3b0277617eb053a41c
ms.sourcegitcommit: 856e42f7d5125d094fa84390bc43048808276b57
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/07/2019
ms.locfileid: "73787095"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序定义可替换或增强连接字符串关键字的连接属性。 一些连接字符串关键字已由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序指定了默认值。  
  
 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序中可用的关键字列表，请参阅将[连接字符串关键字用于 SQL Server Native Client](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 有关 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 连接属性和驱动程序默认行为的详细信息，请参阅[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
 有关对 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 有效的连接字符串关键字的讨论，请参阅将[连接字符串关键字与 SQL Server Native Client 配合使用](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 当**SQLDriverConnect**_DriverCompletion_参数值为 SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE 或 SQL_DRIVER_COMPLETE_REQUIRED 时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序将从显示的对话框中检索关键字值。 如果关键字值传递到连接字符串中，并且用户未在对话框中更改关键字的值，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序将使用连接字符串中的值。 如果在连接字符串中未设置值，并且用户在对话框中未指定任何值，则驱动程序将使用默认值。  
  
 当任何*DriverCompletion*值需要（或可能需要）驱动程序的 "连接" 对话框的显示时，必须为**SQLDriverConnect**指定有效的*WindowHandle* 。 无效句柄将返回 SQL_ERROR。  
  
 指定 DRIVER 或 DSN 关键字。 ODBC 规定，如果同时指定了这两个关键字，驱动程序将使用左边的关键字，而忽略另一个关键字。 如果指定了驱动程序，或者指定了驱动程序的最左侧，并且**SQLDriverConnect**_DriverCompletion_参数值为 SQL_DRIVER_NOPROMPT，则需要 SERVER 关键字和适当的值。  
  
 当指定 SQL_DRIVER_NOPROMPT 时，用户身份验证关键字必须具有值。 驱动程序确保字符串“Trusted_Connection=yes”或 UID 和 PWD 关键字存在。  
  
 如果*DriverCompletion*参数值为 SQL_DRIVER_NOPROMPT 或 SQL_DRIVER_COMPLETE_REQUIRED 并且语言或数据库来自连接字符串，并且两者都无效，则**SQLDriverConnect**返回 SQL_ERROR。  
  
 如果*DriverCompletion*参数值为 SQL_DRIVER_NOPROMPT 或 SQL_DRIVER_COMPLETE_REQUIRED，并且语言或数据库来自 ODBC 数据源定义并且要么无效，则**SQLDriverConnect**将使用默认语言或指定用户 ID 的数据库并返回 SQL_SUCCESS_WITH_INFO。  
  
 如果*DriverCompletion*参数值为 SQL_DRIVER_COMPLETE 或 SQL_DRIVER_PROMPT 并且语言或数据库无效，则**SQLDriverConnect**将重新将对话框。  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>对高可用性、灾难恢复的 SQLDriverConnect 支持  
 有关使用**SQLDriverConnect**连接到 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)] 群集的详细信息，请参阅[SQL Server Native Client 对高可用性、灾难恢复的支持](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>对服务主体名称 (SPN) 的 SQLDriverConnect 支持  
 SQLDDriverConnect 将使用 ODBC Login 对话框 boxwhen 提示已启用。 这允许为主体服务器及其故障转移伙伴输入 SPN。  
  
 SQLDriverConnect 将接受新的连接字符串关键字**ServerSPN**和**FailoverPartnerSPN**，并将识别 SQL_COPT_SS_SERVER_SPN 和 SQL_COPT_SS_FAILOVER_PARTNER_SPN 的新连接属性。  
  
 当多次指定某个连接属性值时，以编程方式设置的值优先于 DSN 中的值和连接字符串中的值。 DSN 中的值优先于连接字符串中的值。  
  
 当打开连接时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 将 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 和 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 设置为用于打开此连接的身份验证方法。  
  
 有关 Spn 的详细信息，请参阅[客户端&#40;连接&#41; &#40;中的服务主体&#41;名称 spn ODBC](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)。  
  
## <a name="examples"></a>示例  
 以下调用说明了**SQLDriverConnect**所需的最少数据量：  
  
```  
SQLDriverConnect(hdbc, hwnd,  
    (SQLTCHAR*) TEXT("DRIVER={SQL Server Native Client 10};"), SQL_NTS, szOutConn,  
    MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
```  
  
 以下连接字符串演示了在 SQL_DRIVER_NOPROMPT *DriverCompletion*参数值时所需的最小数据量：  
  
```  
"DSN=Human Resources;Trusted_Connection=yes"  
  
"FILEDSN=HR_FDSN;Trusted_Connection=yes"  
  
"DRIVER={SQL Server Native Client 10};SERVER=(local);Trusted_Connection=yes"  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQLDriverConnect 函数](https://go.microsoft.com/fwlink/?LinkId=59340)   
 [ODBC API 实现细节](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SET ANSI_NULLS (Transact-SQL)](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING (Transact-SQL)](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [设置 ANSI_WARNINGS &#40;transact-sql&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
