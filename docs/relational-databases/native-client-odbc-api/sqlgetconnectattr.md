---
title: SQLGetConnectAttr |Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
apitype: DLLExport
helpviewer_keywords:
- SQLGetConnectAttr function
ms.assetid: 26e4e69a-44fd-45e3-b47a-ae39184f041b
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 153b5f73ea753639a7617f5de6d942dae40fadda
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/15/2018
ms.locfileid: "51660535"
---
# <a name="sqlgetconnectattr"></a>SQLGetConnectAttr
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序定义了特定于驱动程序的连接属性。 某些特性可供**SQLGetConnectAttr**，，该函数用于报告其当前设置。 有关建立连接，或使用设置该属性后，这些属性不保证之前报告的值[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
 本主题列出只读属性。 有关其他信息[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Native Client ODBC 驱动程序特定的连接属性，请参阅[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)。  
  
## <a name="sqlcoptssconnectiondead"></a>SQL_COPT_SS_CONNECTION_DEAD  
 SQL_COPT_SS_CONNECTION_DEAD 属性报告与服务器的连接的状态。 驱动程序将查询网络，以获得连接的当前状态。  
  
> [!NOTE]  
>  标准 ODBC 连接属性 SQL_ATTR_CONNECTION_DEAD 返回连接的最近状态。 这可能不是当前连接状态。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|SQL_CD_TRUE|与服务器的连接已丢失。|  
|SQL_CD_FALSE|连接已打开，可以用于执行语句处理。|  
  
## <a name="sqlcoptssclientconnectionid"></a>SQL_COPT_SS_CLIENT_CONNECTION_ID  
 SQL_COPT_SS_CLIENT_CONNECTION_ID 属性检索客户端连接 ID，该属性可用于查找：  
  
-   XEvents 日志中的诊断信息（如果启用）。  
  
-   连接环形缓冲区中的连接错误信息。  
  
-   数据访问跟踪日志中的诊断信息（如果启用）。  
  
 有关详细信息，请参阅[扩展事件日志中访问诊断信息](../../relational-databases/native-client/features/accessing-diagnostic-information-in-the-extended-events-log.md)。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|SQL_ERROR|连接失败。|  
|SQL_SUCCESS|连接成功。 将在输出缓冲区中找到客户端连接 ID。|  
  
## <a name="sqlcoptssperfdata"></a>SQL_COPT_SS_PERF_DATA  
 SQL_COPT_SS_PERF_DATA 属性返回包含当前驱动程序性能统计信息的 SQLPERF 结构的指针。 **SQLGetConnectAttr**将返回 NULL，如果未启用性能日志记录。 驱动程序不会动态更新 SQLPERF 结构中的统计信息。 调用**SQLGetConnectAttr**每次需要刷新性能统计信息。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|NULL|未启用性能记录。|  
|任何其他值|SQLPERF 结构的指针。|  
  
## <a name="sqlcoptssperfquery"></a>SQL_COPT_SS_PERF_QUERY  
 如果启用对长时间运行查询的记录，则 SQL_COPT_SS_PERF_QUERY 属性返回 TRUE。 如果查询记录不处于活动状态，则请求返回 FALSE。  
  
## <a name="sqlcoptssuserdata"></a>SQL_COPT_SS_USER_DATA  
 SQL_COPT_SS_USER_DATA 属性检索用户数据指针。 用户数据存储在客户端拥有的内存中，并在每次连接时进行记录。 如果尚未设置用户数据指针，则返回 SQL_UD_NOTSET（NULL 指针）。  
  
|ReplTest1|Description|  
|-----------|-----------------|  
|SQL_UD_NOTSET|未设置用户数据指针。|  
|任何其他值|用户数据的指针。|  
  
## <a name="sqlgetconnectattr-support-for-service-principal-names-spns"></a>对服务主体名称 (SPN) 的 SQLGetConnectAttr 支持  
 SQLGetConnectAttr 可以用于查询新的连接属性 SQL_COPT_SS_SERVER_SPN、 SQL_COPT_SS_FAILOVER_PARTNER_SPN、 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 和 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 的值。 （SQLGetConnectOption 还可查询这些值。）  
  
 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 仅对使用 Windows 身份验证的打开的连接可用。  
  
 如果尚未设置 SQL_COPT_SS_SERVER_SPN 或 SQL_COPT_SS_FAILOVER_PARTNER，则返回默认值（空字符串）。  
  
 有关 Spn 的详细信息，请参阅[服务主体名称&#40;的 Spn&#41;客户端连接中&#40;ODBC&#41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md)。  
  
## <a name="see-also"></a>请参阅  
 [SQLGetConnectAttr 函数](https://go.microsoft.com/fwlink/?LinkId=59347)   
 [ODBC API 实现的详细信息](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)   
 [SET QUOTED_IDENTIFIER (Transact-SQL)](../../t-sql/statements/set-quoted-identifier-transact-sql.md)   
 [SET ANSI_NULLS (Transact-SQL)](../../t-sql/statements/set-ansi-nulls-transact-sql.md)   
 [SET ANSI_PADDING (Transact-SQL)](../../t-sql/statements/set-ansi-padding-transact-sql.md)   
 [SET ANSI_WARNINGS &#40;Transact SQL&#41;](../../t-sql/statements/set-ansi-warnings-transact-sql.md)  
  
  
