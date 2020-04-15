---
title: SQLDriver连接 |微软文档
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
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 8d1455f0b91313ea137ec9c13a2d318fba0807b3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2020
ms.locfileid: "81302539"
---
# <a name="sqldriverconnect"></a>SQLDriverConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序定义可替换或增强连接字符串关键字的连接属性。 一些连接字符串关键字已由 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序指定了默认值。  
  
 有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序中可用的关键字列表，请参阅[使用与 SQL Server 本机客户端的连接字符串关键字](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 有关[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]连接属性和驱动程序默认行为的详细信息，请参阅[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
 有关对[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端有效的连接字符串关键字的讨论，请参阅[使用与 SQL Server 本机客户端的连接字符串关键字](../../relational-databases/native-client/applications/using-connection-string-keywords-with-sql-server-native-client.md)。  
  
 当**SQLDriverConnect**_驱动程序完成_参数值SQL_DRIVER_PROMPT、SQL_DRIVER_COMPLETE 或SQL_DRIVER_COMPLETE_REQUIRED时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]本机客户端 ODBC 驱动程序将从显示的对话框中检索关键字值。 如果关键字值传递到连接字符串中，并且用户未在对话框中更改关键字的值，则 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序将使用连接字符串中的值。 如果在连接字符串中未设置值，并且用户在对话框中未指定任何值，则驱动程序将使用默认值。  
  
 当任何*驱动程序完成*值需要（或可能需要）显示驱动程序的连接对话框时，必须为**SQLDriverConnect**提供有效的*WindowHandle。* 无效句柄将返回 SQL_ERROR。  
  
 指定 DRIVER 或 DSN 关键字。 ODBC 规定，如果同时指定了这两个关键字，驱动程序将使用左边的关键字，而忽略另一个关键字。 如果指定了 DRIVER，或者是两个中最左侧的，并且**SQLDriverConnect**_驱动程序完成_参数值SQL_DRIVER_NOPROMPT，则需要 SERVER 关键字和适当的值。  
  
 当指定 SQL_DRIVER_NOPROMPT 时，用户身份验证关键字必须具有值。 驱动程序确保字符串“Trusted_Connection=yes”或 UID 和 PWD 关键字存在。  
  
 如果*Driver 完成*参数值SQL_DRIVER_NOPROMPT或SQL_DRIVER_COMPLETE_REQUIRED，并且语言或数据库来自连接字符串，并且其中一个无效，**则 SQLDriverConnect**返回SQL_ERROR。  
  
 如果*Driver 完成*参数值SQL_DRIVER_NOPROMPT或SQL_DRIVER_COMPLETE_REQUIRED，并且语言或数据库来自 ODBC 数据源定义，并且无效 **，SQLDriverConnect**使用默认语言或数据库进行指定的用户 ID 并返回SQL_SUCCESS_WITH_INFO。  
  
 如果*驱动程序完成*参数值为SQL_DRIVER_COMPLETE或SQL_DRIVER_PROMPT，并且语言或数据库无效 **，SQLDriverConnect**将重新显示该对话框。  
  
## <a name="sqldriverconnect-support-for-high-availability-disaster-recovery"></a>对高可用性、灾难恢复的 SQLDriverConnect 支持  
 有关使用**SQLDriverConnect**连接到[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]群集的详细信息，请参阅 SQL [Server 本机客户端支持以进行高可用性、灾难恢复](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。  
  
## <a name="sqldriverconnect-support-for-service-principal-names-spns"></a>对服务主体名称 (SPN) 的 SQLDriverConnect 支持  
 启用提示时，SQLDDriverConnect 将使用 ODBC 登录对话框。 这允许为主体服务器及其故障转移伙伴输入 SPN。  
  
 SQLDriverConnect 将接受新的连接字符串关键字**ServerSPN**和**故障转移合作伙伴SPN，** 并将SQL_COPT_SS_SERVER_SPN和SQL_COPT_SS_FAILOVER_PARTNER_SPN识别新的连接属性。  
  
 当多次指定某个连接属性值时，以编程方式设置的值优先于 DSN 中的值和连接字符串中的值。 DSN 中的值优先于连接字符串中的值。  
  
 当打开连接时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 将 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 和 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 设置为用于打开此连接的身份验证方法。  
  
 有关 SPN 的详细信息，请参阅[客户端连接中&#40;ODBC&#41;中的服务主体名称&#40;SPN&#41;。 ](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)  
  
## <a name="examples"></a>示例  
 以下调用说明了**SQLDriverConnect**所需的最少数据量：  
  
```  
SQLDriverConnect(hdbc, hwnd,  
    (SQLTCHAR*) TEXT("DRIVER={SQL Server Native Client 10};"), SQL_NTS, szOutConn,  
    MAX_CONN_OUT, &cbOutConn, SQL_DRIVER_COMPLETE);  
```  
  
 当*驱动程序完成*参数值SQL_DRIVER_NOPROMPT时，以下连接字符串说明了所需的最小数据：  
  
```  
"DSN=Human Resources;Trusted_Connection=yes"  
  
"FILEDSN=HR_FDSN;Trusted_Connection=yes"  
  
"DRIVER={SQL Server Native Client 10};SERVER=(local);Trusted_Connection=yes"  
```  
  
## <a name="see-also"></a>另请参阅  
 [SQLDriver连接功能](https://go.microsoft.com/fwlink/?LinkId=59340)   
 [ODBC API 实施详细信息](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [&#40;交易-SQL&#41;ANSI_NULLS设置](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [set ANSI_PADDING&#40;转算-SQL&#41;](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS (Transact-SQL)](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
