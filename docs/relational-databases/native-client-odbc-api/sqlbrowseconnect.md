---
title: SQLBrowseConnect |Microsoft 文档
ms.custom: ''
ms.date: 03/14/2017
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
- SQLBrowseConnect function
ms.assetid: 57faf388-c7ca-4696-9845-34e0a10cc5f7
caps.latest.revision: 54
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 400097362ec6364d7a7b0d6f13cd3e62bb4d6b87
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/03/2018
---
# <a name="sqlbrowseconnect"></a>SQLBrowseConnect
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  **SQLBrowseConnect**分为三个级别的连接信息使用可以进行分类的关键字。 对于每个关键字，下表指示是否返回有效值列表以及该关键字是否可选。  
  
## <a name="level-1"></a>级别 1  
  
|关键字|是否返回列表？|是否可选？|Description|  
|-------------|--------------------|---------------|-----------------|  
|DSN|N/A|否|返回的数据源名称**SQLDataSources**。 如果使用 DRIVER 关键字，则无法使用 DSN 关键字。|  
|DRIVER|N/A|否|Microsoft® [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC 驱动程序名称是 {[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 11}。 如果使用 DSN 关键字，则无法使用 DRIVER 关键字。|  
  
## <a name="level-2"></a>级别 2  
  
|关键字|是否返回列表？|是否可选？|Description|  
|-------------|--------------------|---------------|-----------------|  
|SERVER|是|否|数据源所驻留网络上的服务器名称。 可以输入术语 "(local)" 作为服务器，在此情况下，即使此为非联网版本，也可以使用 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 的本地副本。|  
|UID|否|是|用户登录 id。|  
|PWD|否|是（取决于用户）|用户指定密码。|  
|APP|否|是|名称的应用程序调用**SQLBrowseConnect**。|  
|WSID|否|是|工作站 id。 通常，这是运行应用程序的计算机的网络名称。|  
  
## <a name="level-3"></a>级别 3  
  
|关键字|是否返回列表？|是否可选？|Description|  
|-------------|--------------------|---------------|-----------------|  
|DATABASE|是|是|名称[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]数据库。|  
|LANGUAGE|是|是|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 使用的区域语言。|  
  
 **SQLBrowseConnect**忽略的 ODBC 数据源定义中存储的数据库和语言关键字的值。 如果数据库或连接字符串中指定的语言传递给**SQLBrowseConnect**是无效的**SQLBrowseConnect**返回 SQL_NEED_DATA 和等级 3 连接属性。  
  
 以下属性，通过调用设置[SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md)，确定返回的结果集**SQLBrowseConnect**。  
  
|Attribute|Description|  
|---------------|-----------------|  
|SQL_COPT_SS_BROWSE_CONNECT|如果设置为 SQL_MORE_INFO_YES， **SQLBrowseConnect**返回扩展的服务器属性字符串。<br /><br /> 以下是返回一个扩展字符串的示例**SQLBrowseConnect**:<br /><br /> <br /><br /> `ServerName\InstanceName;Clustered:No;Version:8.00.131`<br /><br /> <br /><br /> 在此字符串中，分号用于分隔与服务器有关的各部分信息， 逗号用于分隔不同的服务器实例。|  
|SQL_COPT_SS_BROWSE_SERVER|如果指定服务器名称，则**SQLBrowseConnect**将返回指定的服务器的信息。 如果 SQL_COPT_SS_BROWSE_SERVER 设置为 NULL， **SQLBrowseConnect**在域中返回的所有服务器的信息。<br /><br /> <br /><br /> 请注意，由于网络问题而**SQLBrowseConnect**可能未收到及时的响应来自所有服务器。 因此，每个请求所返回的服务器列表都可能不同。|  
|SQL_COPT_SS_BROWSE_CACHE_DATA|如果 SQL_COPT_SS_BROWSE_CACHE_DATA 属性设置为 SQL_CACHE_DATA_YES，当缓冲区长度不足以容纳结果时，您可以提取块区中的数据。 SQLBrowseConnect BufferLength 参数中指定此长度。<br /><br /> 当有更多的数据可用时，将返回 SQL_NEED_DATA。 如果检索不到更多的数据，将返回 SQL_SUCCESS。<br /><br /> 默认值是 SQL_CACHE_DATA_NO。|  
  
## <a name="sqlbrowseconnect-support-for-high-availability-disaster-recovery"></a>对高可用性、灾难恢复的 SQLBrowseConnect 支持  
 有关详细信息使用**SQLBrowseConnect**连接到[!INCLUDE[ssHADR](../../includes/sshadr-md.md)]群集，请参阅[高可用性、 灾难恢复的 SQL Server Native Client Support](../../relational-databases/native-client/features/sql-server-native-client-support-for-high-availability-disaster-recovery.md)。  
  
## <a name="sqlbrowseconnect-support-for-service-principal-names-spns"></a>对服务主体名称 (SPN) 的 SQLBrowseConnect 支持  
 当打开连接时，[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client 将 SQL_COPT_SS_MUTUALLY_AUTHENTICATED 和 SQL_COPT_SS_INTEGRATED_AUTHENTICATION_METHOD 设置为用于打开此连接的身份验证方法。  
  
 有关 Spn 的详细信息，请参阅[服务主体名称 & #40;Spn & #41;在客户端连接 & #40; ODBC & #41;](../../relational-databases/native-client/odbc/service-principal-names-spns-in-client-connections-odbc.md).  
  
## <a name="change-history"></a>更改历史记录  
  
|更新内容|  
|---------------------|  
|介绍了 SQL_COPT_SS_BROWSE_CACHE_DATA。|  
  
## <a name="see-also"></a>另请参阅  
 [SQLBrowseConnect 函数](http://go.microsoft.com/fwlink/?LinkId=59329)   
 [ODBC API 实现详细信息](../../relational-databases/native-client-odbc-api/odbc-api-implementation-details.md)  
  
  
